1. Gateway（网关）—— 整个系统的控制中枢

主要功能：监听消息通道（WhatsApp、Telegram、Discord、Slack 等），接收用户指令 → 路由给 Agent → 执行工具 → 回消息。
简要实现方法：
用 Node.js 写成一个持久后台进程，默认监听本地端口（127.0.0.1:18789）。
通过 WebSocket RPC 统一管理所有通道（channels）和代理（agents）。
支持多通道适配器（extensions/telegram、extensions/whatsapp 等），每个通道插件化。
收到消息后，触发 agentic loop（代理循环）。


2. Agentic Loop（ReAct 风格的代理循环）—— 自主决策与行动的核心

主要功能：Reason + Act 循环，让 AI 能“想一想 → 做一件事 → 看结果 → 再想”直到任务完成。
简要实现方法（经典的单次循环流程）：
上下文组装（Context Assembly）：从 MEMORY.md、对话历史、workspace 文件、长期记忆中拉取相关内容，压缩到模型上下文窗口内（有 compaction reserve 机制防止爆 token）。
模型推理（LLM Call）：把系统提示（SOUL.md + AGENTS.md）+ 当前上下文 + 可用工具描述发给 LLM（支持 Claude、GPT、Gemini、本地模型等）。
工具调用（Tool Call）：模型返回工具调用指令（JSON 格式），Gateway 执行对应工具。
结果反馈：工具执行结果再塞回上下文，继续下一轮循环（可多轮）。
流式回复（Streaming）：边思考边把最终文字流式发回聊天软件。

这是 OpenClaw 最核心的“像人一样做事”的实现逻辑，几乎所有自主能力都靠这个循环。

3. Skills（技能）—— 模块化能力扩展

主要功能：让 Agent 能做具体事（如发邮件、写代码、管日历、爬网页等）。
简要实现方法：
每个 Skill 就是一个 Markdown 文件（放在 ~/.openclaw/workspace/skills/ 目录）。
文件里包含：
什么时候用这个技能（触发条件描述）
如何用（自然语言指令 + 可选的 JS/Shell 脚本）
参数 schema（给 LLM 看的工具描述）

Agent 看到任务时，会根据 SOUL.md 和 TOOLS.md 决定调用哪些 Skill。
支持热加载：放进目录后无需重启 Gateway 即可使用。
社区有 ClawHub（技能市场），一键安装几千个现成技能。


4. Memory & Workspace（记忆与工作区）—— 无数据库的持久化方案

主要功能：记住长期信息、对话历史、学习成果。
简要实现方法：
全部用纯 Markdown 文件存储在 ~/.openclaw/workspace/ 目录下（local-first 哲学）。
关键文件：
SOUL.md：人格/性格/行为准则（系统提示核心）
AGENTS.md：Agent 的角色、目标、约束
MEMORY.md：长期记忆（手动或自动追加）
USER.md：用户信息、偏好
sessions/ 目录：每个会话的 JSONL 历史

上下文加载时按优先级读取这些文件，自动压缩/总结旧内容。


5. Heartbeat（心跳）与自主主动性

主要功能：即使没人发消息，Agent 也能定时醒来做事（比如每天检查邮件、提醒日程）。
简要实现方法：
Gateway 内置一个可配置的定时器（cron 风格）。
每隔 N 分钟触发一次“空闲思考”循环：读取待办、检查 MEMORY 中的计划 → 决定是否行动。
常用于“主动汇报”“定时任务”“监控提醒”等场景。


6. Tool Execution（工具执行层）

主要功能：安全执行模型决定的操作。
简要实现方法：
内置工具：shell 执行、文件读写、浏览器控制（Playwright）、日历/邮件接口。
技能工具：每个 Skill 可带 JS 函数或 shell 脚本。
执行沙箱：最新版本加强了权限控制（可配置最小权限、黑名单、人工确认高危操作）。


总结：最简架构一句话描述