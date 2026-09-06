# mattpocock/skills — Evaluation Report 2026

**Created:** September 5, 2026
**Version:** 1.0
**Evaluated for:** Hermes Agent (Nous Research) + Claude Code + Codex + GitHub-issue Kanban workflow
**Source:** https://github.com/mattpocock/skills (252,612 ⭐ · #1 publisher on skills.sh, 19.6M installs)

---

## 🎯 Executive Summary

mattpocock/skills is the most-installed skills collection in the world ("Skills for Real Engineers. Straight from my .agents directory"). Its 37 skills share a coherent philosophy: **engineering workflow driven by the issue tracker**, inspired by John Ousterhout's *A Philosophy of Software Design* (deep modules, design docs, relentless "grilling" of plans before implementation).

**Key findings for our stack:**
1. **Excellent fit with our GitHub-issue Kanban workflow** — a whole family (triage / to-tickets / to-spec / wayfinder / code-review) is built around routing issues through state machines and generating agent-ready tickets. This is the strongest reason to adopt.
2. **Near-zero overlap with our existing Hermes skills** — only tdd / code-review / diagnosing-bugs have close relatives locally (different methodology); ~30 skills are genuinely new.
3. **Agent-agnostic by default** — most skills are plain SKILL.md + bash/gh-CLI (agentskills standard), compatible with Hermes. Only a handful are Claude-Code-specific (marked below).
4. **HTML-report outputs** (improve-codebase-architecture, teach) fit our html-* report family naturally.
5. **Caveat:** several files are tiny pointers (grill-me 157B, implement 433B, research 794B, handoff 894B) that load logic from siblings/references — install the whole family, not isolated files. Some "in-progress" skills are unfinished.

---

## 📋 Part 1: Full Evaluation (37 skills)

Legend: ✅ Install · 🔄 Alternative to existing (choose one) · ⚠️ Situational · ❌ Skip

### engineering/ (18)

| Skill | Purpose | Relation to existing Hermes skills | Verdict |
|-------|---------|-----------------------------------|---------|
| **ask-matt** | Router: which skill/flow fits your situation | No equivalent (meta-skill) | ✅ with family |
| **code-review** | Review diffs from a base point along "Standards" axes; posts findings to issue tracker | Local: `requesting-code-review`, `github-code-review` (different framing: ours = pre-submit self-review & PR review; his = post-change standards audit via issues) | 🔄 optional |
| **codebase-design** | Shared vocabulary for designing "deep modules" (Ousterhout); find deepening opportunities | No equivalent. Philosophy docs for architecture work | ✅ high |
| **diagnosing-bugs** | Diagnosis loop for hard bugs & perf regressions | Local: `systematic-debugging` (same goal, different process — ours is TDD-style bisect loop) | 🔄 pick one |
| **domain-modeling** | Build/sharpen domain model; write CONTEXT.md + glossary | No equivalent. Complements our AGENTS.md culture | ✅ medium |
| **grill-with-docs** | Relentless interview that also produces ADRs + glossary | No equivalent (combines grilling + documentation) | ✅ with grilling |
| **implement** | Implement work from a spec/ticket set (pointer file) | No equivalent (local `plan`/`spike` cover earlier phases) | ✅ |
| **improve-codebase-architecture** | Scan codebase → **visual HTML report** of deepening opportunities → grill through your pick | No equivalent. HTML output matches our html-* report skills | ✅ high |
| **prototype** | Throwaway prototype to answer a design question | Local: `spike` (similar intent, lighter) | 🔄 optional |
| **research** | Investigate vs high-trust primary sources → Markdown in repo | Local research family (arxiv/web/chinese-web) is broader; this one is engineering-scoped | ⚠️ optional |
| **resolving-merge-conflicts** | Walk through an in-progress git merge/rebase conflict | No equivalent | ✅ low |
| **setup-matt-pocock-skills** | One-time setup: issue labels, domain layout, Claude Code config | Setup for adopting the whole system in Claude Code | ⚠️ only if full adoption |
| **tdd** | Red-green-refactor, issue-centric TDD | Local: `test-driven-development` (obra lineage). Both solid; his is ticket-flavored | 🔄 keep local |
| **to-spec** | Synthesize conversation → spec → publish to issue tracker | No equivalent (we spec via `writing-plans`/markdown, not issues) | ✅ high |
| **to-tickets** | Break plan/spec into "tracer-bullet" tickets with blocking edges → issue tracker | No equivalent. Directly feeds our Kanban workers | ✅ high |
| **triage** | Route issues/PRs through a state machine; write agent-ready briefs | Local: `kanban-orchestrator`/`kanban-worker` (similar spirit, homegrown) | ✅ high (or merge ideas) |
| **wayfinder** | Plan work >1 session → map of decision tickets on issue tracker | No equivalent (multi-session planning via issues) | ✅ high |
| **wizard** | Generate interactive bash wizard for human-only steps (provisioning etc.) | No equivalent | ✅ medium |

### productivity/ (7)

| Skill | Purpose | Relation to existing skills | Verdict |
|-------|---------|----------------------------|---------|
| **grill-me / grilling** | Relentless Socratic interview to stress-test a plan/decision | No equivalent (his #1–2 downloads). Great pre-implementation gate for Kanban | ✅ high |
| **handoff** | Compact conversation → handoff doc for another agent/session | Local: `subagent-driven-development` has its own handoff; his is standalone/doc-based — pairs well with herdr-style agent handovers | ✅ high |
| **teach** | Teach a concept interactively, produces HTML report | No equivalent (co-op prep uses slideshow skill instead) | ⚠️ medium |
| **to-questionnaire** | Turn an unanswerable decision into a questionnaire | No equivalent | ⚠️ low |
| **wait-what** | Re-pitch when a message didn't land | Meta-communication skill | ⚠️ low |
| **writing-for-agents** | Write docs for agents (AGENTS.md/CLAUDE.md/skills) — ⚠️ Claude-Code-flavored | We maintain agenticSkills + many skills → directly useful | ✅ high |

### in-progress/ (8) — unfinished, treat as experimental

| Skill | Notes | Verdict |
|-------|-------|---------|
| claude-handoff | Background-agent handoff (preview) | ❌ wait for stable |
| implement-spec | Duplicate of engineering/implement | ❌ skip |
| loop-me | "Grill me about specs for workflows I want to build" | ⚠️ try later |
| retro | Session retrospective (Claude Code) | ⚠️ optional for CC lanes |
| setup-ts-deep-modules | Wire dependency-cruiser; TS deep-module enforcement | ⚠️ useful for digital-human-adk (TS/Next.js) |
| writing-beats / writing-fragments / writing-shape | Fiction/article writing trio | ❌ off-domain |

### misc/ (4)

| Skill | Notes | Verdict |
|-------|-------|---------|
| git-guardrails-claude-code | Claude Code hooks blocking dangerous git commands | ⚠️ install if Claude Code used by team |
| migrate-to-shoehorn | One-off TS assertion migration | ❌ skip |
| scaffold-exercises | Teaching exercise scaffolds | ❌ skip |
| setup-pre-commit | Husky + lint-staged + typecheck + tests | ⚠️ per-repo |

---

## 🛠️ Part 2: Recommended Adoption Package

**Wave 1 — Kanban/issue workflow suite (highest ROI, matches our GitHub-issue lanes):**
`triage` · `to-tickets` · `to-spec` · `wayfinder` · `implement` · `handoff`

**Wave 2 — Thinking/quality gates:**
`grill-me` (grilling) · `grill-with-docs` · `codebase-design` · `improve-codebase-architecture` · `domain-modeling`

**Wave 3 — Utilities:**
`writing-for-agents` · `resolving-merge-conflicts` · `wizard` · `ask-matt` (with family)

**Keep existing (don't duplicate):** `test-driven-development` (local), `systematic-debugging` (local), `spike` (local) — unless his variants prove better in a side-by-side trial.

---

## ⚠️ Part 3: Integration Notes & Caveats

1. **Format compatibility**: standard SKILL.md (agentskills spec) → installs into `~/.hermes/skills/<name>/` exactly like our existing skills. No adaptation needed for the agent-agnostic ones.
2. **Issue-tracker assumption**: Wave 1 skills assume GitHub issues as the system of record — matches our Kanban (we already run issue-driven lanes).
3. **Claude Code-specific** (skip or keep for CC lanes only): `git-guardrails-claude-code`, `retro`, `setup-matt-pocock-skills`, `writing-for-agents` (still useful for Hermes skill authoring).
4. **Pointer files**: small SKILL.md files load logic from siblings — always install family members together.
5. **Evaluation depth caveat**: this report is based on frontmatter + structural signatures of all 37 skills, not full-text reads of every one. Pilot Wave 1 on one project and E2E-test before company-wide adoption.
6. **Provenance risk**: single-maintainer repo (Matt Pocock). Excellent quality signal (252K ⭐, 19.6M installs, weekly churn) but bus-factor = 1.

---

## 📎 Part 4: References

- Repo: https://github.com/mattpocock/skills
- Leaderboard context: `AI-Skills/AI_SKILLS_MARKETPLACE_LEADERBOARD_REPORT_2026_EN.md`
- Related: `Devin/GITHUB_COPILOT_SKILLS_SETUP_GUIDE_2026.md` · `nihaixia` skill (installed, same format)
