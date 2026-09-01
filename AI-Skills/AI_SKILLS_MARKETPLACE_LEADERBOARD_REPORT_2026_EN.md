# AI Skills Marketplace Leaderboard Research Report 2026

**Created:** August 29, 2026
**Version:** 1.0
**Data Source:** skills.sh (Vercel Agent Skills Directory) leaderboard API — complete All-Time dataset (600 skills)
**Data Retrieved:** August 29, 2026

---

## 🎯 Executive Summary

AI Skills (Agent Skills) emerged in 2025–2026 as a **portable instruction-package standard for AI agents**: domain workflows (TDD, code review, frontend design, database setup…) are packaged as a single SKILL.md file that any agent supporting the standard (Claude Code, GitHub Copilot, Codex, Cursor, **Hermes/Nous Research**, and 30+ others) can install with one command and load on demand.

This report is based on the **official skills.sh leaderboard** (which tracks installs through the `npx skills` CLI and agent integrations). We retrieved the complete dataset of **600 skills / 129,378,304 total installs** and analyzed the all-time download ranking, publisher landscape, and install trends.

**Key takeaways:**
1. **Matt Pocock alone accounts for 15% of all installs** (52 skills, 19.6M total) — development-workflow skills (TDD/grill/handoff) are the biggest demand
2. **Official vendors have entered en masse**: Anthropic (3.0M), Microsoft Azure (13.7M), Vercel, Google, Prisma, Supabase all publish official skills
3. **Feishu (Lark) ships 28 skills with near-identical install counts (~640K each)** — a tell-tale sign of enterprise bulk/preloaded installs; discount these when reading personal-adoption signals
4. **skills.sh officially supports Nous Research (Hermes)** — Hermes users can install marketplace skills directly via `npx skills`

---

## 📋 Part 1: Market Overview

### 1.1 Ecosystem Map

| Platform | Role | Notes |
|----------|------|-------|
| **skills.sh** | De-facto skill directory + leaderboard + install stats | Operated by Vercel; tracks CLI installs |
| **anthropics/skills** | Official skill library (20 skills) | 172,916 ⭐; the ecosystem benchmark |
| **agentskills.io** | Open format spec (0.2.0) | Cross-agent compatibility standard |
| **`npx skills` CLI** | Install tool | `npx skills add <repo> --skill <name>` |
| **Vendor agent-skills repos** | Official skill sources | Microsoft/Vercel/Google/Prisma/Supabase/Stripe… |

### 1.2 Supported Agents (20 listed on skills.sh)

Claude Code, Cursor, Codex, GitHub Copilot, Windsurf, Gemini, Cline, AMP, Antigravity, OpenClaw, Droid, Goose, Kilo, Kiro CLI, **Nous Research (Hermes)**, OpenCode, Roo, Trae, VS Code, Zed.

---

## 🏆 Part 2: All-Time Download Leaderboard (Top 30)

Retrieved from the skills.sh leaderboard API (All Time), including 8-week install trends.

| # | Skill | Source | Total Installs |
|---|-------|--------|----------------|
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
| 13–36 | lark-* series (doc/base/drive/im/calendar/sheets, 24 skills) | open.feishu.cn | ~640K each |
| 37 | anti-ui-slop | uizze.com | 604,240 |
| 38 | web-design-guidelines | vercel-labs/agent-skills | 596,960 |
| 39 | grilling | mattpocock/skills | 594,137 |
| 41 | teach | mattpocock/skills | 571,459 |
| 42–55 | azure-* series (foundry/diagnostics/ai/deploy/validate, etc.) | microsoft/azure-skills | ~555K each |
| 58 | domain-modeling | mattpocock/skills | 541,311 |
| 61 | remotion-best-practices | remotion-dev/skills | 504,402 |
| 62–65 | ai-video/image-generation, ai-avatar-video, twitter-automation | skills-101/superpowers | ~500K each |
| 70 | caveman | juliusbrussee/caveman | 471,833 |
| 73 | code-review | mattpocock/skills | 459,288 |
| 83 | design-taste-frontend | leonxlnx/taste-skill | 429,265 |
| 128 | skill-creator | anthropics/skills | 368,658 |
| 193 | shadcn | shadcn/ui | 271,675 |

> The full 600-entry list is archived in `ai-skills-leaderboard.json` (a byproduct of this research).

---

## 📊 Part 3: Publisher Landscape

### 3.1 Top 15 Publishers (by total installs)

| Publisher | Total Installs | Skills | Type |
|-----------|----------------|--------|------|
| mattpocock/skills | 19,616,993 | 52 | Individual (community) |
| open.feishu.cn (Lark) | 16,950,706 | 28 | Enterprise official |
| microsoft/azure-skills | 13,650,929 | 32 | Enterprise official |
| runcomfy-agent-skills | 10,933,989 | 30 | Community (AI media generation) |
| larksuite/cli | 10,739,680 | 27 | Enterprise official |
| heygen-com/hyperframes | 6,360,410 | 38 | Enterprise official |
| coreyhaines31/marketingskills | 4,395,865 | 61 | Individual (community) |
| rigorpilot-skills | 3,975,585 | 11 | Community |
| leonxlnx/taste-skill | 3,673,543 | 13 | Individual (community) |
| vercel-labs/skills | 3,203,119 | 1 | Enterprise official |
| anthropics/skills | 2,995,862 | 18 | Official (Anthropic) |
| obra/superpowers | 2,969,217 | 14 | Individual (community) |
| skills-101/superpowers | 2,406,893 | 10 | Community |
| juliusbrussee/caveman | 2,374,900 | 8 | Individual (community) |
| vercel-labs/agent-skills | 2,232,657 | 9 | Enterprise official |

### 3.2 Key Insights

1. **The Matt Pocock effect**: a single individual captured 15% of the entire board with 52 high-quality skills. His grill series (code-review interrogation), tdd, handoff (agent-to-agent transition), and triage (issue triage) hit the core pain points of AI-collaborative workflows.
2. **Official vs. community**: 167 of 600 skills carry an official flag. Enterprise publishers (Microsoft/Vercel/Feishu/HeyGen) enter with *series* of skills; communities enter with *single hits*.
3. **Domain distribution**:
   - Development workflow (TDD/Review/Architecture/Handoff) → most stable installs
   - Frontend design (frontend-design, web-design-guidelines, anti-ui-slop, taste-skill) → second-largest category
   - AI media generation (runcomfy 30, heygen 38) → largest by skill count
   - Platform integration (Azure/Lark/Prisma/Supabase/Firebase/Stripe) → official strongholds
4. **Easter egg**: herdr's skill (a previous research subject) is also on the board (#591, 37,460 installs).

### 3.3 Data Caveats

- Install counts come from skills.sh telemetry (CLI + agent integration reports); **git-clone usage is not counted**, so real usage is higher
- **All 28 Lark skills show nearly identical counts (641K–643K)** → strongly suggests enterprise bulk/preloaded installs; do not read them as individual-demand signals
- This board is All-Time; skills.sh also offers Trending (24h) and Hot tabs

---

## 🛠️ Part 4: Recommendations for Your Team

### 4.1 Priority Skills by Use Case

| Use Case | Skill | Source | Installs |
|----------|-------|--------|----------|
| Skill discovery | find-skills | vercel-labs/skills | 3.2M |
| TDD development | tdd | mattpocock/skills | 813K |
| Code-review interrogation | grill-me / grill-with-docs | mattpocock/skills | 1.0M / 874K |
| Agent handoff | handoff | mattpocock/skills | 715K |
| Issue triage | triage | mattpocock/skills | 706K |
| Frontend design standards | frontend-design / web-design-guidelines | anthropics / vercel-labs | 841K / 597K |
| Architecture improvement | improve-codebase-architecture | mattpocock/skills | 840K |
| Browser automation | agent-browser | vercel-labs/agent-browser | 765K |
| Socratic learning | grilling | mattpocock/skills | 594K |

### 4.2 Overlap with Hermes Built-in Skills

Many top-ranked skills are already built into Hermes with the same lineage (from the obra/superpowers ecosystem): `writing-plans`, `requesting-code-review`, `systematic-debugging`, `test-driven-development`, `plan`, `spike`, `subagent-driven-development`, etc. — **the team's existing Hermes skill stack already covers the top of the board in the development-workflow category**; no re-install needed. The main gaps are **frontend-design skills** (frontend-design, anti-ui-slop) and **platform-integration skills** (Prisma/Supabase/Firebase), which can be added per project.

### 4.3 Installation

```bash
# Works with Hermes / Claude Code / Copilot and 20+ agents
npx skills add <repo> --skill <skill-name>          # project level
npx skills add <repo> --skill <skill-name> -g       # global (personal)
```

---

## 📎 Part 5: Appendix

- **Data file**: `ai-skills-leaderboard.json` (600 entries incl. 8-week trends)
- **Official directory**: https://skills.sh
- **Format spec**: https://schemas.agentskills.io/discovery/0.2.0/schema.json
- **Official skill library**: https://github.com/anthropics/skills
- **Related report**: `Devin/GITHUB_COPILOT_SKILLS_SETUP_GUIDE_2026.md` (Copilot Skills setup guide)
