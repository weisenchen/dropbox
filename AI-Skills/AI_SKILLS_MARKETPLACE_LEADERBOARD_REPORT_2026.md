# AI Skills Marketplace 排行榜研究报告 2026

**Created:** August 29, 2026
**Version:** 1.0
**Data Source:** skills.sh (Vercel Agent Skills Directory) leaderboard API — All Time 完整資料（600 個 skills）
**数据抓取日期:** 2026-08-29

---

## 🎯 Executive Summary

AI Skills（Agent Skills）是 2025–2026 年興起的**可攜式 Agent 指令包標準**：把專業工作流（TDD、Code Review、前端設計、數據庫設定…）包成一個 SKILL.md 檔，讓任何支援該標準的 AI Agent（Claude Code、GitHub Copilot、Codex、Cursor、**Hermes/Nous Research** 等 30+ 家）一鍵安裝、按需載入。

本報告基於 **skills.sh 官方排行榜**（追蹤 `npx skills` CLI 與各家 Agent 整合的安裝量）抓取完整 **600 個 skills / 總安裝 129,378,304 次**，解析全時段下載量排名、發行商格局與安裝趨勢。

**核心結論：**
1. **Matt Pocock 一人獨占 15% 安裝量**（52 個 skills，合計 1,960 萬）——開發流程類（TDD/grill/handoff）是最大需求
2. **官方陣營全面進場**：Anthropic（3.0M）、Microsoft Azure（13.7M）、Vercel、Google、Prisma、Supabase 等都有官方 skills
3. **飛書 Lark 系列 28 個 skills 數字齊整（~64 萬/個）**——企業批量預裝特徵明顯，個人安裝榜需打折看待
4. **skills.sh 已官方支援 Nous Research（Hermes）**——Hermes 用戶可直接用 `npx skills` 安裝

---

## 📋 Part 1: 市場概覽

### 1.1 生態系地圖

| 平台 | 定位 | 備註 |
|------|------|------|
| **skills.sh** | 事實上的技能目錄 + 排行榜 + 安裝統計 | Vercel 營運，追蹤 CLI 安裝量 |
| **anthropics/skills** | 官方技能庫（20 個） | 172,916 ⭐，生態系標竿 |
| **agentskills.io** | 開放格式規範（0.2.0） | 跨 Agent 相容標準 |
| **`npx skills` CLI** | 安裝工具 | `npx skills add <repo> --skill <name>` |
| **各廠商 agent-skills repos** | 官方技能來源 | Microsoft/Vercel/Google/Prisma/Supabase/Stripe… |

### 1.2 支援的 Agent（skills.sh 列出的 20 家）

Claude Code、Cursor、Codex、GitHub Copilot、Windsurf、Gemini、Cline、AMP、Antigravity、OpenClaw、Droid、Goose、Kilo、Kiro CLI、**Nous Research（Hermes）**、OpenCode、Roo、Trae、VS Code、Zed。

---

## 🏆 Part 2: 全時段下載量排行榜（Top 30）

資料抓取自 skills.sh leaderboard API（All Time），總安裝數含 8 週趨勢。

| # | Skill | 來源 | 總安裝 |
|---|-------|------|--------|
| 1 | find-skills | vercel-labs/skills | 3,203,119 |
| 2 | grill-me | mattpocock/skills | 1,025,984 |
| 3 | grill-with-docs | mattpocock/skills | 874,421 |
| 4 | frontend-design | anthropics/skills | 841,498 |
| 5 | improve-codebase-architecture | mattpocock/skills | 840,349 |
| 6 | tdd | mattpocock/skills | 812,857 |
| 7 | agent-browser | vercel-labs/agent-browser | 764,988 |
| 8 | setup-matt-pocock-skills | mattpocock/skills | 749,365 |
| 9 | handoff | mattpocock/skills | 715,133 |
| 10 | triage | mattpocock/skills | 706,302 |
| 11 | prototype | mattpocock/skills | 697,186 |
| 12 | vercel-react-best-practices | vercel-labs/agent-skills | 680,647 |
| 13–36 | lark-* 系列（doc/base/drive/im/calendar/sheets 等 24 個） | open.feishu.cn | ~64 萬/個 |
| 37 | anti-ui-slop | uizze.com | 604,240 |
| 38 | web-design-guidelines | vercel-labs/agent-skills | 596,960 |
| 39 | grilling | mattpocock/skills | 594,137 |
| 41 | teach | mattpocock/skills | 571,459 |
| 42–55 | azure-* 系列（foundry/diagnostics/ai/deploy/validate 等） | microsoft/azure-skills | ~55.5 萬/個 |
| 58 | domain-modeling | mattpocock/skills | 541,311 |
| 61 | remotion-best-practices | remotion-dev/skills | 504,402 |
| 62–65 | ai-video/image-generation、ai-avatar-video、twitter-automation | skills-101/superpowers | ~50 萬/個 |
| 70 | caveman | juliusbrussee/caveman | 471,833 |
| 73 | code-review | mattpocock/skills | 459,288 |
| 83 | design-taste-frontend | leonxlnx/taste-skill | 429,265 |
| 128 | skill-creator | anthropics/skills | 368,658 |
| 193 | shadcn | shadcn/ui | 271,675 |

> 完整 600 名清單已存檔：`ai-skills-leaderboard.json`（本次研究副產物）。

---

## 📊 Part 3: 發行商格局

### 3.1 Top 15 發行商（依總安裝）

| 發行商 | 總安裝 | Skills 數 | 類型 |
|--------|--------|----------|------|
| mattpocock/skills | 19,616,993 | 52 | 個人（社群） |
| open.feishu.cn（飛書） | 16,950,706 | 28 | 企業官方 |
| microsoft/azure-skills | 13,650,929 | 32 | 企業官方 |
| runcomfy-agent-skills | 10,933,989 | 30 | 社群（AI 生圖/影片） |
| larksuite/cli | 10,739,680 | 27 | 企業官方 |
| heygen-com/hyperframes | 6,360,410 | 38 | 企業官方 |
| coreyhaines31/marketingskills | 4,395,865 | 61 | 個人（社群） |
| rigorpilot-skills | 3,975,585 | 11 | 社群 |
| leonxlnx/taste-skill | 3,673,543 | 13 | 個人（社群） |
| vercel-labs/skills | 3,203,119 | 1 | 企業官方 |
| anthropics/skills | 2,995,862 | 18 | 官方（Anthropic） |
| obra/superpowers | 2,969,217 | 14 | 個人（社群） |
| skills-101/superpowers | 2,406,893 | 10 | 社群 |
| juliusbrussee/caveman | 2,374,900 | 8 | 個人（社群） |
| vercel-labs/agent-skills | 2,232,657 | 9 | 企業官方 |

### 3.2 關鍵洞察

1. **Matt Pocock 效應**：個人開發者靠 52 個高品質 skills 拿下全榜 15%。他的 grill 系列（程式碼審查提問）、tdd、handoff（Agent 交接）、triage（Issue 分類）精準打中「AI 協作工作流」痛點。
2. **官方 vs 社群**：600 個中 167 個帶官方標記；企業官方（Microsoft/Vercel/Feishu/HeyGen）以**系列化**批量進榜，社群以**單品爆款**進榜。
3. **領域分布**：
   - 開發流程（TDD/Review/Architecture/Handoff）→ 安裝量最穩
   - 前端設計（frontend-design、web-design-guidelines、anti-ui-slop、taste-skill）→ 第二大類
   - AI 媒體生成（runcomfy 30 個、heygen 38 個）→ 數量最多
   - 平台整合（Azure/Lark/Prisma/Supabase/Firebase/Stripe）→ 官方主場
4. **彩蛋**：herdr（前次研究對象）的 skill 也在榜上（#591，37,460 安裝）。

### 3.3 資料可信度注意

- 安裝數來自 skills.sh telemetry（CLI + Agent 整合回報），**git clone 直接使用的不計入**，實際用量更高
- **Lark 系列 28 個 skills 安裝數幾乎相同（641K–643K）** → 高度疑似企業批量預裝/內建計數，不建議視為個人需求訊號
- 本榜為 All Time；skills.sh 另有 Trending（24h）與 Hot 分榜

---

## 🛠️ Part 4: 對團隊的建議

### 4.1 值得優先安裝的 Top Skills（依使用場景）

| 場景 | Skill | 來源 | 安裝量 |
|------|-------|------|--------|
| 找技能 | find-skills | vercel-labs/skills | 3.2M |
| TDD 開發 | tdd | mattpocock/skills | 813K |
| 程式碼審查提問 | grill-me / grill-with-docs | mattpocock/skills | 1.0M / 874K |
| Agent 交接 | handoff | mattpocock/skills | 715K |
| Issue 分類 | triage | mattpocock/skills | 706K |
| 前端設計規範 | frontend-design / web-design-guidelines | anthropics / vercel-labs | 841K / 597K |
| 架構改進 | improve-codebase-architecture | mattpocock/skills | 840K |
| 瀏覽器自動化 | agent-browser | vercel-labs/agent-browser | 765K |
| 學習（Grok 風格） | grilling | mattpocock/skills | 594K |

### 4.2 與 Hermes 內建 skills 的對照

榜單上多個熱門技能在 Hermes 已內建同源版本（來自 obra/superpowers 生態）：`writing-plans`、`requesting-code-review`、`systematic-debugging`、`test-driven-development`、`plan`、`spike`、`subagent-driven-development` 等——**團隊現有的 Hermes 技能棧已覆蓋排行榜最前段的開發流程類**，無需重複安裝；缺口主要在**前端設計類**（frontend-design、anti-ui-slop）與**平台整合類**（Prisma/Supabase/Firebase），可按實際專案補充。

### 4.3 安裝方式

```bash
# 支援 Hermes / Claude Code / Copilot 等 20+ Agent
npx skills add <repo> --skill <skill-name>          # 專案級
npx skills add <repo> --skill <skill-name> -g       # 全域（個人）
```

---

## 📎 Part 5: 附錄

- **資料檔案**：`ai-skills-leaderboard.json`（600 條，含 8 週安裝趨勢）
- **官方目錄**：https://skills.sh
- **格式規範**：https://schemas.agentskills.io/discovery/0.2.0/schema.json
- **官方技能庫**：https://github.com/anthropics/skills
- **相關報告**：`Devin/GITHUB_COPILOT_SKILLS_SETUP_GUIDE_2026.md`（Copilot Skills 設定指南）
