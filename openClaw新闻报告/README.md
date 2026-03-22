我写这份文件主要就是想要理清楚我们到底要报道什么新闻
# 主题：openClaw
* [opencLaw的源代码仓库](https://github.com/openclaw/openclaw)
* [安装技能的地方](https://github.com/openclaw/clawhub)
# 介绍面(应该介绍什么内容)
## ‘龙虾热’在程序员中的前身？
Claude,copolit自动代码编辑ai工具

## [openClaw的改名风波]

## ‘龙虾热’如何兴起？
* 兴起随时间变化的过程
![gitHub流行图.svg](%E7%9B%B8%E5%85%B3%E5%9B%BE%E7%89%87/gitHub%E6%B5%81%E8%A1%8C%E5%9B%BE.svg)
* 在二月份发生了什么？
  * [创始人加入openAI，openClaw与openAI合作](https://techcrunch.com/2026/02/15/openclaw-creator-peter-steinberger-joins-openai/)  
  * 2026年2月14日，彼得·斯坦伯格宣布自己将加入OpenAI，而OpenClaw则以基金会形式作为开源项目存续。斯坦伯格表示“我想要改变世界，而非打造一家大型企业，与OpenAI合作是实现这一目标的最快途径”
* [深圳市政府支持](https://mp.weixin.qq.com/s/TmfxEDyG-OaHw6kGr-9tCQ)
## open claw这种代理类型的人工智能与聊天型人工智能有什么区别？
## 为什么是龙虾？
* 龙虾和其他的ai工具有什么不一样的地方？(**有决定权，可以彻底帮你把事情做完**)
  * (内置能力)
      * 长期记忆能力
      * 定时任务能力
      * 灵魂能力
  * 插件扩展能力,在clawhub上你可以为龙虾添加很多能力[Clawhub](https://github.com/openclaw/clawhub)
* 可以接入社交软件，借助社交软件迅速传播
* 描述简单清晰，易于传播
### 官方的能力介绍
[openClaw仓库描述页面.md](%E7%9B%B8%E5%85%B3%E6%96%87%E4%BB%B6/openClaw%E4%BB%93%E5%BA%93%E6%8F%8F%E8%BF%B0%E9%A1%B5%E9%9D%A2.md)
* 简要的介绍
  * Gateway（總指揮中心）： 這是整個系統對外的門面與核心路由器。它負責管理所有的連線、帳號認證以及環境設定，確保外部指令能正確傳達到內部。
  * Agent（大腦與執行長）： 這是真正在「思考」並決定下一步該做什麼的代理程式。當收到任務時，Agent 會分析上下文，決定要呼叫哪個 AI 模型以及使用哪些工具來完成目標。
  * Skills（手腳與工具箱）： 這是 OpenClaw 最強大也最需謹慎管理的擴充模組（OpenClaw skill）。透過安裝不同的 Skill，AI 才能真正接觸「外在世界」，例如學會讀取本地檔案、操作 Google 行事曆，或是發送 WhatsApp 訊息。
  * Memory（專屬筆記本）： 傳統 AI 聊完就忘，但 OpenClaw 預設透過本地資料庫（如 SQLite）建立長期記憶。這讓 AI 能記住你們昨天的對話脈絡，以及過去執行任務的偏好設定。
  * Cron（排程鬧鐘）： 如果你需要 AI 在特定的時間點做事（例如：每週五下午 5 點自動彙整本週報表），Cron 就會在這個時間準時喚醒系統執行任務。
  * Heartbeat（心跳與巡邏員）： 這是讓 AI 具備「主動性」的關鍵。Heartbeat 會在背景定時跳動（喚醒系統），讓 AI 主動去檢查指定的頻道或信箱「現在有沒有新任務需要處理？」，而非只能被動等待指令。
## ‘龙虾’潜藏风险
### 提示词注入攻击
[工信部文件](https://mp.weixin.qq.com/s/mRWlFkiq9gaqX1oVuu9Ceg)
### 逻辑死锁
### 隐私泄露
[隐私噩梦](https://news.northeastern.edu/2026/02/10/open-claw-ai-assistant/)
### 上下文压缩出错
[元安全研究员的 AI 代理意外删除了她的邮件 _PCMag --- Meta Security Researcher's AI Agent Accidentally Deleted Her Emails _ PCMag.html](%E7%9B%B8%E5%85%B3%E5%9B%BE%E7%89%87/%E5%85%83%E5%AE%89%E5%85%A8%E7%A0%94%E7%A9%B6%E5%91%98%E7%9A%84%20AI%20%E4%BB%A3%E7%90%86%E6%84%8F%E5%A4%96%E5%88%A0%E9%99%A4%E4%BA%86%E5%A5%B9%E7%9A%84%E9%82%AE%E4%BB%B6%20_PCMag%20---%20Meta%20Security%20Researcher%27s%20AI%20Agent%20Accidentally%20Deleted%20Her%20Emails%20_%20PCMag.html)
