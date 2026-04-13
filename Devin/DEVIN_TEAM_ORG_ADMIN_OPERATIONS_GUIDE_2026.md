# Devin Team Organization Admin: Operations Guide 2026

**Created:** April 13, 2026  
**Version:** 1.0  
**Scope:** Team-level operations (excluding infrastructure, org setup, user access - handled by firm-wide admins)  
**Sources:** Official Devin Docs + Cognition AI Announcements + Industry Best Practices

---

## 🎯 Executive Summary

**Purpose:** This guide is for **Team Organization Admins** who manage day-to-day Devin operations within their team. Infrastructure, organization setup, and user access control are managed by firm-wide administrators.

**What Team Admins Control:**
- ✅ ACU usage optimization within allocated budget
- ✅ Session management and best practices
- ✅ Knowledge base creation and organization
- ✅ Repository configuration and secrets
- ✅ Playbook/Skills development for team workflows
- ✅ MCP server usage (within enterprise allowlist)
- ✅ Team workflow optimization
- ✅ Usage monitoring and reporting to firm-wide admins

**What Firm-Wide Admins Control (Out of Scope):**
- ❌ Infrastructure setup (SSO, VPC, etc.)
- ❌ Organization creation and structure
- ❌ User access control and permissions
- ❌ Enterprise API key management
- ❌ Global secret rotation
- ❌ Audit log configuration

---

## 📋 Part 1: Role & Responsibilities

### Team Admin vs Firm-Wide Admin

| Responsibility | Team Admin | Firm-Wide Admin |
|----------------|------------|-----------------|
| **ACU Budget** | Optimize within allocation | Set org-level limits |
| **Session Management** | Daily oversight, best practices | Hard caps, policies |
| **Knowledge Base** | Create, organize, maintain | Enterprise distribution |
| **Repositories** | Connect, configure, secrets | OAuth, global secrets |
| **Playbooks/Skills** | Team-specific workflows | Enterprise skills |
| **MCP Servers** | Use within allowlist | Allowlist enforcement |
| **User Access** | ❌ No access | ✅ Full control |
| **Org Structure** | ❌ No access | ✅ Full control |
| **Infrastructure** | ❌ No access | ✅ Full control |

### Daily Responsibilities Checklist

```
Morning (15 min):
□ Review overnight session completions
□ Check ACU usage vs. daily budget
□ Review any failed sessions
□ Address team questions from Slack/Teams

Throughout Day:
□ Monitor active high-ACU sessions
□ Help team with complex task delegation
□ Review playbook effectiveness
□ Update knowledge base as needed

End of Day (15 min):
□ Review daily ACU consumption
□ Archive completed sessions
□ Note any issues for firm-wide admin
□ Plan next day's priorities
```

---

## 💰 Part 2: ACU Management (Within Allocation)

### Understanding Your ACU Budget

**Typical Team Allocation:**
```
Small Team (1-5 devs):     200-400 ACU/month
Medium Team (6-12 devs):   400-800 ACU/month
Large Team (13+ devs):     800-1500 ACU/month

Daily Budget = Monthly ACU / 22 working days
Example: 500 ACU/month ÷ 22 = ~23 ACU/day
```

### ACU Consumption by Task Type

| Task Type | Typical ACU | When to Use |
|-----------|-------------|-------------|
| **Simple Q&A** | 0.5-2 ACU | Quick questions, code explanation |
| **File Edit** | 2-10 ACU | Single file changes, bug fixes |
| **Feature Implementation** | 10-50 ACU | New endpoints, components |
| **Multi-file Refactor** | 30-100 ACU | Extract modules, rename patterns |
| **Test Generation** | 20-80 ACU | Unit tests, integration tests |
| **Managed Devins (5 workers)** | 100-500 ACU | Large migrations, bulk operations |
| **DeepWiki Generation** | 10-200 ACU | Documentation (varies by depth) |

### ACU Optimization Strategies

**1. Right-Size Your Sessions**

```
❌ Expensive: One giant session for everything
✅ Efficient: Multiple focused sessions

Example:
Instead of: "Refactor the entire auth module" (150 ACU)
Do:
  - Session 1: "Add token refresh logic" (30 ACU)
  - Session 2: "Update session management" (30 ACU)
  - Session 3: "Add refresh tests" (25 ACU)
  Total: 85 ACU (43% savings)
```

**2. Use Plan Mode for Large Tasks**

```
Plan Mode (reading only) → Free or minimal ACU
Implementation Mode → Full ACU consumption

Process:
1. Start in Plan Mode: "Analyze the auth flow and propose changes"
2. Review the plan (no implementation yet)
3. Approve plan → Implementation begins
4. Result: No ACU wasted on wrong approaches
```

**3. Leverage Knowledge Base**

```
Without Knowledge: Devin relearns your patterns each session
With Knowledge: Devin applies team conventions immediately

ACU Savings: 20-30% per session (less back-and-forth)
```

**4. Batch Similar Tasks**

```
❌ Inefficient: 10 sessions for 10 similar bug fixes
✅ Efficient: 1 Managed Devins session with 10 workers

Example:
"Fix the null pointer exceptions in these 10 files"
→ 1 coordinator + 10 workers = ~200 ACU total
→ vs. 10 separate sessions = ~300 ACU total
```

### Daily ACU Monitoring

**Usage Dashboard View:**
```
Team ACU Dashboard (Example):
┌─────────────────────────────────────────────────────────┐
│  Team: Platform Engineering                              │
│  Monthly Budget: 500 ACU                                 │
│  Used: 287 ACU (57%) | Remaining: 213 ACU                │
│  Days Left: 14                                           │
│                                                          │
│  Daily Average: 13 ACU | Today: 18 ACU                   │
│  On Track: ✅ (projected 400/500 ACU)                    │
├─────────────────────────────────────────────────────────┤
│  Top Users (This Week)                                   │
│  user1@co.com: 45 ACU | user2@co.com: 38 ACU            │
│  user3@co.com: 32 ACU | user4@co.com: 28 ACU            │
├─────────────────────────────────────────────────────────┤
│  Top Repositories                                        │
│  backend-api: 89 ACU | frontend-web: 67 ACU             │
│  mobile-app: 45 ACU | infra: 23 ACU                     │
└─────────────────────────────────────────────────────────┘
```

**Alert Thresholds:**
```
50% of monthly budget → Normal check-in
75% of monthly budget → Review high-consumption sessions
90% of monthly budget → Request additional ACU or pause non-critical work
100% of monthly budget → Sessions blocked until next cycle
```

### Weekly ACU Report Template

```markdown
## ACU Usage Report - Week of [Date]

**Budget Status:**
- Monthly Allocation: 500 ACU
- Used This Week: 87 ACU
- Used Month-to-Date: 287 ACU (57%)
- Projected Month-End: 400 ACU (80%)

**Top Consuming Sessions:**
1. "Migrate auth to OAuth2" - 45 ACU (completed)
2. "Add payment webhook tests" - 32 ACU (completed)
3. "Refactor user service" - 28 ACU (in progress)

**Optimization Actions:**
- Switched 3 large tasks to Plan Mode first
- Created playbook for common PR reviews
- Archived 15 old sessions

**Issues/Requests:**
- None this week
- / Request additional 100 ACU for Q2 project
```

---

## 📝 Part 3: Session Management

### Session Lifecycle

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   PLANNING  │───▶│  EXECUTION  │───▶│   REVIEW    │───▶│  ARCHIVE    │
│             │    │             │    │             │    │             │
│ Define task │    │ Monitor     │    │ Check PR    │    │ Export if   │
│ Set scope   │    │ Progress    │    │ Merge if OK │    │ important   │
│             │    │ Intervene   │    │             │    │             │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
     5-10 min        Variable          10-15 min          2-5 min
```

### Best Practices for Session Delegation

**1. Clear Task Definition**

```
❌ Vague: "Fix the bugs in the payment module"
✅ Clear: "Fix the 3 failing tests in payment_processor_test.py.
          Error: 'NoneType has no attribute amount'.
          Expected: All 3 tests pass, no regressions in other tests."
```

**2. Provide Context**

```
❌ No Context: "Add a new endpoint"
✅ With Context: "Add GET /api/v2/users/{id}/preferences endpoint.
                 Follow the pattern in user_controller.py lines 45-80.
                 Use the same response format as /api/v2/users/{id}.
                 Add tests in test_user_preferences.py."
```

**3. Set Checkpoints**

```
For tasks >30 ACU:
"After you complete the schema changes, stop and show me the migration
before proceeding to the model updates."

Benefits:
- Catch issues early
- Prevent wasted ACU on wrong path
- Better control over output
```

### Session Categories

**Use Devin's Categorization Feature (April 2026):**

| Category | Use Case | Example |
|----------|----------|---------|
| **Bug Fix** | Fixing failures | "Fix null pointer in auth" |
| **Feature** | New functionality | "Add user preferences API" |
| **Refactor** | Code improvement | "Extract payment service" |
| **Tests** | Test generation | "Add unit tests for auth" |
| **Docs** | Documentation | "Update API documentation" |
| **Review** | Code review | "Review PR #1234" |
| **Research** | Investigation | "Analyze error patterns" |

### Pin Important Sessions

**When to Pin:**
```
✅ Pin:
- Complex debugging sessions (reference for future)
- Architecture decision sessions
- Team playbook creation sessions
- Sessions with valuable learnings

❌ Don't Pin:
- Simple one-off tasks
- Failed/abandoned sessions
- Routine PR reviews
```

**How to Pin:**
```
1. Open session
2. Click three-dot menu (⋮)
3. Select "Pin Session"
4. Access pinned sessions from sidebar

Limit: 20-50 pinned sessions per org (check your limit)
```

### Archive Old Sessions

**Why Archive:**
- Keeps workspace organized
- Reduces visual clutter
- Maintains performance

**When to Archive:**
```
Sessions >30 days old → Archive
Sessions with completed PRs → Archive after merge
Failed sessions >7 days old → Archive or delete
```

---

## 📚 Part 4: Knowledge Base Management

### Knowledge vs Playbooks vs Skills

| Type | Purpose | Scope | Example |
|------|---------|-------|---------|
| **Knowledge** | Team context, conventions | Always available | "Our API versioning strategy" |
| **Playbooks** | Repeated workflows | On-demand | "PR Review Checklist" |
| **Skills** | Specialized procedures | On-demand | "Playwright Test Generator" |

### Creating Knowledge Notes

**Structure:**
```markdown
# Knowledge Note: API Versioning Strategy

## Overview
We use URL-based versioning (api/v1/, api/v2/) for all public endpoints.

## When to Create New Version
- Breaking changes to request/response schema
- Removing deprecated fields
- Changing authentication requirements

## Migration Process
1. Create v2 endpoint alongside v1
2. Mark v1 as deprecated in docs
3. Notify consumers via changelog
4. Maintain v1 for 90 days minimum
5. Remove v1 after migration complete

## Examples
- v1 → v2 migration: /api/v1/users → /api/v2/users
- Response format: See user_response_v2.json
```

**Organization:**
```
Knowledge Base/
├── Architecture/
│   ├── API Versioning
│   ├── Database Schema
│   └── Service Boundaries
├── Conventions/
│   ├── Code Style
│   ├── Naming Conventions
│   └── Error Handling
├── Workflows/
│   ├── Deployment Process
│   ├── Code Review
│   └── Incident Response
└── Domain Knowledge/
    ├── Payment System
    ├── User Management
    └── Third-party Integrations
```

### Knowledge Best Practices

**1. Keep It Current**

```
Review Schedule:
- Critical docs (API, auth): Monthly
- Conventions: Quarterly
- Workflows: After each process change

Action:
□ Add "Last Updated" date to each note
□ Set calendar reminder for reviews
□ Archive outdated notes
```

**2. Make It Discoverable**

```
✅ Good titles:
- "API Versioning Strategy"
- "Database Naming Conventions"
- "Payment Integration Guide"

❌ Bad titles:
- "Stuff we do"
- "Random notes"
- "Important thing"
```

**3. Include Examples**

```
Knowledge without examples:
"We use dependency injection"

Knowledge with examples:
"We use dependency injection:

```python
# ✅ Good
class UserService:
    def __init__(self, db: Database, cache: Cache):
        self.db = db
        self.cache = cache

# ❌ Bad - Don't instantiate dependencies inside methods
class UserService:
    def get_user(self, id: str):
        db = Database()  # Don't do this
        return db.query(...)
```
```

### Knowledge Search Optimization

**April 2026 Feature: Auto-Expand Search**
```
When searching, folders containing matches auto-expand.

Optimization Tips:
- Use consistent terminology in titles
- Add relevant tags/keywords
- Cross-reference related notes
- Use folder hierarchy logically
```

---

## 🔧 Part 5: Repository Management

### Repository Configuration

**What Team Admins Can Configure:**
```
✅ Within Your Control:
- Repository connection (if OAuth already set up by firm-wide admin)
- Branch protection rules for Devin
- Repository-specific secrets
- Repository custom instructions
- Snapshot/blueprint configuration
```

### Repository Secrets

**Bulk Import (April 2026 Feature):**
```
Previously: Add secrets one at a time
Now: Import multiple secrets at once

Use Cases:
- New repository onboarding
- Secret rotation across repos
- Environment variable updates

Process:
1. Settings → Repositories → [Select Repo]
2. Secrets → Bulk Import
3. Upload JSON/CSV with secret names and values
4. Review and confirm
```

**Secret Types by Repository:**
```
Backend API Repo:
- DATABASE_URL
- REDIS_URL
- JWT_SECRET
- EXTERNAL_API_KEY

Frontend Repo:
- API_BASE_URL
- ANALYTICS_KEY
- FEATURE_FLAGS

Mobile Repo:
- APP_STORE_CREDENTIALS
- PUSH_NOTIFICATION_KEY
- CRASHLYTICS_KEY
```

### Custom Instructions (Per-Repository)

**When to Use:**
```
Use Repository Custom Instructions for:
- Project-specific coding standards
- File structure conventions
- Testing requirements
- Commit message format

Use Skills for:
- Specialized workflows (testing, debugging)
- Reusable procedures across repos
- Task-specific guidance
```

**Example Repository Instructions:**
```markdown
# Repository: backend-api

## Code Style
- Python 3.11+ with type hints
- Follow PEP 8
- Use Black for formatting
- Use Ruff for linting

## Testing
- pytest for all new code
- Minimum 80% coverage
- Mock external services

## API Standards
- RESTful endpoints
- JSON:API response format
- OpenAPI 3.0 documentation

## Commit Messages
- Conventional Commits format
- Include ticket number: "feat(API-123): add user endpoint"
```

### Snapshot & Blueprint Management

**Snapshots:**
```
Purpose: Capture repository state for Devin to understand

When to Update:
- After major refactors
- When adding new services
- After architecture changes

Cancel In-Progress Builds (April 2026):
- Click "Cancel" in snapshot list
- No need to wait for failure
- Saves indexing ACU
```

**Blueprints:**
```
Purpose: Define common workflows for your repo

Examples:
- "Add New API Endpoint"
- "Create Database Migration"
- "Deploy to Staging"

Ordering (April 2026):
- Configure blueprint order in settings
- Most-used blueprints appear first
- Respected across detail rails
```

---

## 📖 Part 6: Playbook & Skills Development

### Creating Team Playbooks

**When to Create a Playbook:**
```
✅ Create Playbook When:
- Same task done 3+ times
- Task has clear steps
- Multiple team members need consistency
- Onboarding new team members

❌ Don't Create When:
- One-time task
- Highly variable process
- Requires significant judgment
```

**Playbook Template:**
```markdown
---
name: pr-review-checklist
description: Standard checklist for reviewing pull requests
---

# PR Review Checklist

## Pre-Review
1. Check PR description is complete
2. Verify linked issue/ticket
3. Confirm tests are included

## Code Review
1. Logic correctness
2. Error handling
3. Security considerations
4. Performance impact
5. Code style compliance

## Testing
1. Unit tests pass
2. Integration tests pass
3. Coverage meets threshold (80%)

## Before Approval
1. Changelog updated
2. Documentation updated
3. Feature flag added (if applicable)
```

### Skills for Team Workflows

**Example: Team Test Generation Skill**
```markdown
---
name: team-test-generator
description: Generate tests following team conventions
---

# Test Generation Guidelines

## Test File Location
- Unit tests: `src/__tests__/{filename}.test.ts`
- Integration tests: `tests/integration/{feature}.test.ts`
- E2E tests: `tests/e2e/{flow}.spec.ts`

## Test Structure
```typescript
describe('Feature Name', () => {
  beforeEach(() => {
    // Setup using test-fixtures.ts
  });

  it('should expected behavior', async () => {
    // Arrange
    // Act
    // Assert
  });
});
```

## Mocking Standards
- Use jest.mock() for external services
- Use test-fixtures.ts for common mocks
- Never mock the system under test

## Coverage Requirements
- Branch coverage: 80% minimum
- Critical paths: 100% required
```

### Skill Distribution Within Team

```
1. Create skill in team organization
2. Test with 2-3 team members
3. Refine based on feedback
4. Document usage in knowledge base
5. Add to team onboarding checklist
6. Request enterprise distribution (if valuable to other teams)
```

---

## 🔌 Part 7: MCP Server Usage

### Using MCP Servers (Within Allowlist)

**Enterprise Allowlist (Firm-Wide Admin Sets):**
```
Typical Allowed MCPs:
✅ GitHub - Repository access, PR management
✅ Linear - Issue tracking, project management
✅ Amplitude - Product analytics
✅ Internal Wiki - Company documentation
✅ Database - Read-only query access
```

**Connecting MCP Servers:**
```
1. Settings → MCP Servers
2. Browse Marketplace (filtered to allowlist)
3. Click "Install" on approved server
4. Complete OAuth flow (if required)
5. Server available in all sessions
```

**Personal MCP Servers (April 2026 Feature):**
```
Purpose: Connect personal productivity tools

Examples:
- Personal Notion workspace
- Individual Todoist account
- Custom internal tools

Limitations:
- No access to org secrets
- Only visible to you
- Audit logged
```

### MCP Usage Best Practices

**1. Use MCPs for Context**
```
Instead of: Pasting 100 lines of API docs
Use: GitHub MCP to fetch file directly

Benefit: Saves context window, always current
```

**2. Combine MCPs for Complex Tasks**
```
Example: "Add analytics for new feature"
- Linear MCP: Get ticket requirements
- GitHub MCP: Read existing analytics code
- Amplitude MCP: Check event naming conventions
- Result: Consistent implementation
```

**3. Monitor MCP Usage**
```
MCP calls consume ACU:
- Simple query: ~1-2 ACU
- Complex operation: ~5-10 ACU
- Bulk operations: ~20-50 ACU

Track in session details
```

---

## 📊 Part 8: Team Workflow Optimization

### Integrating Devin into Team Workflow

**Slack Integration:**
```
Common Patterns:
1. Tag @Devin in bug discussion threads
2. Devin creates investigation session
3. Devin posts findings back to thread
4. Team reviews and approves fix

Example:
[Slack Thread]
User1: "Seeing 500 errors in payment service"
User2: "@Devin can you investigate?"
→ Devin session created
→ Devin: "Found null pointer in line 45. Creating fix..."
→ Devin: "PR created: #1234"
```

**GitHub Integration:**
```
Issue-Driven Workflow:
1. Create GitHub Issue
2. Label: "devin-eligible"
3. Devin picks up issue
4. Devin creates PR
5. Team reviews PR
6. Merge if approved
```

**Daily Standup Integration:**
```
Devin Status Update:
- Sessions completed yesterday: 8
- ACU consumed: 45
- PRs created: 5
- PRs merged: 4
- Blockers: None

Team Discussion:
- Review high-ACU sessions
- Identify optimization opportunities
- Plan today's priorities
```

### Task Triage Framework

```
┌─────────────────────────────────────────────────────────┐
│  TASK TRIAGE DECISION TREE                              │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Is the task well-defined?                              │
│  ├── No → Human clarifies requirements first            │
│  └── Yes ↓                                              │
│                                                         │
│  Is the task <30 min for human?                         │
│  ├── Yes → Human does it (faster than delegation)       │
│  └── No ↓                                               │
│                                                         │
│  Does the task require human judgment?                  │
│  ├── Yes → Human does it                                │
│  └── No ↓                                               │
│                                                         │
│  Is there a playbook/skill for this?                    │
│  ├── No → Create one, then delegate                     │
│  └── Yes ↓                                              │
│                                                         │
│  → Delegate to Devin                                    │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Delegation Decision Matrix

| Task Type | Delegate to Devin? | Notes |
|-----------|-------------------|-------|
| **Bug Fix (clear error)** | ✅ Yes | Provide stack trace |
| **Bug Fix (vague)** | ⚠️ Clarify first | "It's broken" → specify what |
| **New Feature (scoped)** | ✅ Yes | Clear requirements |
| **New Feature (vague)** | ⚠️ Plan mode first | Explore requirements |
| **Code Review** | ✅ Yes | Use PR review playbook |
| **Architecture Decision** | ⚠️ Human-led | Devin provides analysis |
| **Emergency Hotfix** | ✅ Yes | Fast turnaround |
| **Security-Sensitive** | ⚠️ Human review | Always review output |
| **Documentation** | ✅ Yes | Well-suited |
| **Creative/UX** | ❌ Human | Requires judgment |

---

## 📈 Part 9: Reporting to Firm-Wide Admins

### Monthly Report Template

```markdown
## Team Devin Usage Report - [Month Year]

**Team:** Platform Engineering
**Report Period:** April 1-30, 2026

### ACU Summary
- Allocated: 500 ACU
- Used: 423 ACU (85%)
- Remaining: 77 ACU
- Trend: ↑ 12% vs. previous month

### Productivity Metrics
- Sessions Completed: 187
- PRs Created: 94
- PRs Merged: 89 (95% merge rate)
- Average Session ACU: 2.3
- Top 3 ACU Consumers:
  1. "Migration to OAuth2" - 89 ACU
  2. "Payment webhook tests" - 67 ACU
  3. "API documentation update" - 45 ACU

### Optimization Actions
- Created 3 new team playbooks
- Archived 45 old sessions
- Updated 12 knowledge notes
- Conducted team training on Plan Mode

### Issues/Blockers
- None this month
- / Request: Additional 100 ACU for Q2 migration project

### Next Month Plans
- Major project: Database migration (estimated 200 ACU)
- Focus area: Test coverage improvement
- Training: New team member onboarding
```

### Escalation Triggers

**When to Contact Firm-Wide Admin:**
```
🔴 Urgent (Contact Immediately):
- Security concern with Devin output
- Credential exposure in session
- Unauthorized access suspected

🟡 Important (Contact Within 24h):
- ACU budget will be exceeded
- Need additional organization
- Systemic technical issues

🟢 Routine (Include in Monthly Report):
- Optimization suggestions
- Feature requests
- Usage trends
```

### ACU Budget Adjustment Request

```markdown
**ACU Budget Adjustment Request**

**Team:** Platform Engineering
**Current Allocation:** 500 ACU/month
**Requested Allocation:** 700 ACU/month
**Effective Date:** May 1, 2026

**Justification:**
- Q2 database migration project (estimated 150 ACU)
- New team members (3 additional devs)
- Expanded test coverage initiative

**Expected ROI:**
- Migration: 2 weeks → 3 days (saves 40 engineering hours)
- Test coverage: 60% → 85% (reduces production bugs)

**Commitment:**
- Monthly reporting on usage
- Quarterly optimization review
- Share learnings with other teams
```

---

## 🎓 Part 10: Team Enablement

### Onboarding New Team Members

**Day 1 Checklist:**
```
□ Add to organization (firm-wide admin does this)
□ Grant repository access (firm-wide admin does this)
□ Provide team-specific onboarding:
  - Knowledge base overview
  - Team playbooks
  - Repository conventions
  - ACU budget awareness
□ First task: Simple, well-defined bug fix
□ Pair with experienced Devin user for first session
```

**Week 1 Goals:**
```
□ Complete 3-5 simple sessions
□ Understand Plan Mode vs. Implementation
□ Know when to delegate vs. do manually
□ Familiar with team knowledge base
□ Created first PR via Devin
```

**Month 1 Goals:**
```
□ Comfortable with daily Devin usage
□ Contributed to team knowledge base
□ Can identify good delegation candidates
□ Understanding of ACU optimization
□ Independent session management
```

### Team Training Topics

**Session 1: Devin Basics (1 hour)**
```
- What is Devin and when to use it
- Creating your first session
- Writing effective prompts
- Reviewing and merging PRs
```

**Session 2: Advanced Delegation (1 hour)**
```
- Task triage framework
- Plan Mode for large tasks
- Checkpoint strategy
- ACU optimization techniques
```

**Session 3: Team Workflows (1 hour)**
```
- Team playbooks overview
- Knowledge base contribution
- Repository-specific conventions
- MCP server usage
```

### Sharing Best Practices

**Team Knowledge Sharing:**
```
Weekly:
- Share 1 win (successful delegation)
- Share 1 lesson (what didn't work)
- Review high-ACU sessions

Monthly:
- Update team playbooks
- Refresh knowledge base
- Identify optimization opportunities
```

**Cross-Team Sharing:**
```
- Present at engineering all-hands
- Contribute to enterprise knowledge
- Share playbooks with other teams
- Participate in Devin user group
```

---

## 📖 Part 11: Resources

### Official Documentation
- [Devin User Guide](https://docs.devin.ai/user-guide/overview)
- [Knowledge Management](https://docs.devin.ai/knowledge/overview)
- [Playbooks & Skills](https://docs.devin.ai/skills/overview)
- [MCP Marketplace](https://docs.devin.ai/mcp/marketplace)

### Team Resources
- **Internal Wiki:** [Your company's Devin wiki]
- **Team Playbooks:** [Link to your team's playbooks]
- **Knowledge Base:** [Link to your org's knowledge]
- **Slack Channel:** #devin-users

### Tools
- **ACU Dashboard:** Settings → Usage → Team View
- **Session Archive:** Sessions → Filter → Archived
- **Knowledge Search:** Knowledge → Search (auto-expand enabled)

---

## 🎯 Quick Reference

### Daily Checklist
```
□ Review overnight completions
□ Check ACU usage
□ Address team questions
□ Monitor high-ACU sessions
□ Archive old sessions
```

### Session Best Practices
```
□ Define clear scope
□ Provide context
□ Use Plan Mode for large tasks
□ Set checkpoints
□ Review before merge
```

### ACU Optimization
```
□ Batch similar tasks
□ Use knowledge base
□ Right-size sessions
□ Archive old sessions
□ Monitor daily usage
```

### When to Escalate
```
🔴 Security concern → Immediately
🟡 Budget exceeded → Within 24h
🟢 Feature request → Monthly report
```

---

**Last Updated:** April 13, 2026  
**Author:** weisenaibot 🐺  
**License:** Internal use only  
**Scope:** Team-level operations (excludes infrastructure, org setup, user access)
