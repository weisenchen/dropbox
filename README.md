# 📦 Dropbox - Knowledge Repository

个人知识库，归档整理各类技术文档和 AI 相关内容。

## 📁 目录结构

```
dropbox/
├── Devin/              # Devin AI Agent 相关文档
├── AI-Builders/        # AI Builders Digest 摘要
└── README.md
```

## 📚 内容分类

### Devin/
Devin AI Agent 的完整使用指南和最佳实践：

| 文件 | 说明 |
|------|------|
| `DEVIN_SKILLS_STEP_BY_STEP_GUIDE_2026.md` | ⭐ **Skills 完全指南** - 从零开始创建和使用 Devin Skills |
| `DEVIN_MASTER_GUIDE_2026.md` | Devin 完全指南 - 综合入门教程 |
| `DEVIN_COMPLETE_GUIDE_2026.md` | Devin 完整功能指南 |
| `DEVIN_ACU_COST_MANAGEMENT_GUIDE.md` | ACU 成本管理与优化指南 |
| `DEVIN_AGENTS_EFFICIENT_USAGE_GUIDE.md` | 高效使用 Devin 的最佳实践 |
| `DEVIN_MULTI_AGENT_ORCHESTRATION_GUIDE.md` | 多 Agent 编排指南 |
| `DEVIN_ORG_MANAGEMENT_REPORT.md` | 组织管理与协作报告 |
| `DEVIN_PLAYBOOK_SKILLS_GUIDE_EN.md` | Devin Playbook 与 Skills 指南（英文版） |

### AI-Builders/
每日 AI 领域建设者动态摘要（自动更新）：

- `latest.md` - 最新一期摘要
- `ai-builders-digest-*.md` - 历史摘要归档

**内容来源：**
- 🎙️ 5 个 AI Podcast (Latent Space, Training Data, No Priors 等)
- 🐦 25 位 AI Builder 的 X/Twitter 动态 (Sam Altman, Andrej Karpathy, Garry Tan 等)

**更新时间：** 每天晚上 7:00 (America/Toronto)

---

## 🔧 自动化

AI-Builders 内容通过 `follow-builders` skill 自动获取并推送：
- Cron 任务：每天晚上 7 点运行
- 自动生成 digest 并推送到此仓库

---

最后更新：2026-04-13
