# Devin AI Skills: Complete Step-by-Step Guide 2026

**Created:** April 13, 2026  
**Version:** 1.0  
**Sources:** Official Devin Documentation + Coding Agents 101 + Industry Best Practices

---

## 🎯 Quick Start: Your First Devin Skill

### What Are Devin Skills?

**Skills** (also called **Playbooks**) are reusable, shareable task templates that teach Devin how to perform specific workflows consistently. Think of them as custom system prompts optimized for repetitive tasks.

**Key Benefits:**
- ✅ **Consistency** - Same quality output every time
- ✅ **Efficiency** - Save hours on repetitive work
- ✅ **Knowledge Transfer** - Share best practices across team
- ✅ **Automation** - Turn complex workflows into one-click tasks

---

## 📋 Part 1: Understanding Devin Skills Architecture

### How Devin Skills Work

```
┌─────────────────────────────────────────────────────────────┐
│                    User Input                                │
│         "Add unit tests for payment module"                  │
└─────────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                   Devin Skill/Playbook                       │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  Objective: Create comprehensive unit tests          │   │
│  │  Steps: 1. Analyze code 2. Identify edge cases...   │   │
│  │  Specs: 80% coverage, mock external services        │   │
│  │  Forbidden: No hardcoded credentials, no network    │   │
│  └──────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│              Devin's Execution Environment                   │
│   ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────────┐   │
│   │  Shell  │  │   IDE   │  │ Browser │  │   Tests     │   │
│   └─────────┘  └─────────┘  └─────────┘  └─────────────┘   │
└─────────────────────────────────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    Output                                    │
│   • Test files created                                      │
│   • Tests passing                                           │
│   • PR ready for review                                     │
└─────────────────────────────────────────────────────────────┘
```

### Devin's Internal Agent Architecture

Devin uses a **compound AI system** with specialized agents:

| Agent | Role | When It Activates |
|-------|------|-------------------|
| **Planner** | Creates strategy & task breakdown | Every new task |
| **Coder** | Writes actual code | Implementation phase |
| **Critic** | Reviews for bugs & security | Before committing |
| **Debugger** | Fixes failing tests/errors | When errors occur |
| **Browser** | Fetches docs & research | When external info needed |

---

## 🛠️ Part 2: Step-by-Step - Creating Your First Skill

### Step 1: Identify a Repeatable Task

**Good Candidates for Skills:**
- ✅ Writing unit tests for new features
- ✅ Adding API endpoints with standard structure
- ✅ Creating database migrations
- ✅ Code refactoring (JS → TypeScript)
- ✅ Documentation updates
- ✅ Dependency upgrades
- ✅ Bug fix templates for common issues

**Bad Candidates:**
- ❌ One-time exploratory tasks
- ❌ Highly creative/subjective work
- ❌ Tasks requiring frequent human judgment

### Step 2: Document Your Current Process

Before creating a skill, write down how YOU do the task:

```markdown
## My Current Process: Adding Unit Tests

1. Open the file I want to test
2. Identify all public functions/methods
3. For each function:
   - Write happy path test
   - Write edge case tests
   - Write error handling tests
4. Mock external dependencies (APIs, databases)
5. Run tests, ensure they pass
6. Check code coverage (target: 80%+)
7. Commit with descriptive message
```

### Step 3: Structure Your Skill

Use this proven template:

```markdown
# Skill Name: Unit Test Generator

## Objective
Generate comprehensive unit tests for any Python/JavaScript module with 80%+ coverage.

## Context
This skill helps maintain code quality by automatically creating tests for new features.

## Steps
1. **Analyze Target File**
   - Read the source file completely
   - Identify all public functions/classes
   - Note external dependencies (APIs, databases, services)

2. **Design Test Structure**
   - Create test file following project conventions
   - Set up test fixtures and mocks
   - Import necessary testing libraries

3. **Implement Tests**
   - Write happy path tests for each function
   - Add edge case tests (null, empty, boundary values)
   - Add error handling tests
   - Mock all external dependencies

4. **Validate**
   - Run test suite
   - Verify all tests pass
   - Check code coverage meets 80% threshold
   - Fix any failing tests

5. **Deliver**
   - Commit test files with clear message
   - Create PR with test summary
   - Tag relevant reviewers

## Specifications
- Test file naming: `test_<filename>.py` or `<filename>.test.js`
- Coverage requirement: 80% minimum
- Mock external services using pytest-mock or Jest
- Include docstrings for complex test cases

## Forbidden Actions
- Never hardcode credentials or API keys
- Never skip error handling tests
- Never modify source files (tests only)
- Never commit without running tests first

## Required from User
- Path to the file needing tests
- Any specific edge cases to focus on
- Access to test database (if applicable)

## Common Pitfalls
- Forgetting to mock async functions
- Missing edge cases for user input validation
- Not testing error scenarios
```

### Step 4: Test and Refine Your Skill

**Testing Process:**

1. **Run with Simple Task First**
   ```
   "Use the Unit Test Generator skill on src/utils/helpers.py"
   ```

2. **Review Output**
   - Are tests comprehensive?
   - Do they follow the spec?
   - Is coverage adequate?

3. **Iterate on the Skill**
   - Add missing steps
   - Clarify ambiguous instructions
   - Add more forbidden actions if needed

4. **Test with Complex Scenarios**
   ```
   "Use the Unit Test Generator skill on src/payment/stripe_integration.py"
   ```

---

## 📚 Part 3: Advanced Skill Patterns

### Pattern 1: Multi-Stage Skills

For complex workflows, create checkpoint-based skills:

```markdown
# Full-Stack Feature Implementation

## Phase 1: Database Layer
1. Design schema changes
2. Create migration files
3. Update models
**CHECKPOINT**: Wait for user approval before proceeding

## Phase 2: Backend API
1. Create new endpoints
2. Add request validation
3. Write integration tests
**CHECKPOINT**: Run tests, wait for approval

## Phase 3: Frontend
1. Create UI components
2. Connect to API
3. Add error handling
**CHECKPOINT**: Preview deployment review

## Phase 4: Documentation
1. Update API docs
2. Add usage examples
3. Update changelog
```

### Pattern 2: Conditional Skills

Skills that adapt based on context:

```markdown
# Bug Fix Skill

## Triage
IF error has stack trace:
  → Analyze stack trace, locate failing code
ELSE IF error is UI-related:
  → Check browser console, inspect DOM
ELSE:
  → Ask user for more details

## Fix
IF database issue:
  → Check migrations, connection strings
IF API issue:
  → Verify endpoints, authentication
IF logic issue:
  → Review algorithm, edge cases

## Validate
Run relevant test suite before marking complete
```

### Pattern 3: Skills with External Tools

Integrate MCPs (Model Context Protocols) and custom tools:

```markdown
# Production Deployment Skill

## Pre-Deployment Checks
1. Run full test suite (via MCP: test-runner)
2. Check CI/CD pipeline status (via MCP: github-actions)
3. Verify staging deployment healthy (via MCP: health-check)

## Deployment
1. Create release tag
2. Deploy to production (via MCP: deploy-command)
3. Monitor error rates for 5 minutes

## Rollback Plan
IF error rate > 1%:
  → Trigger automatic rollback
  → Notify team via Slack
  → Create incident report
```

---

## 🔗 Part 4: Integrating Skills into Workflows

### Slack Integration

**Setup:**
1. Add Devin to your Slack workspace
2. Configure webhook endpoints
3. Create skill trigger commands

**Usage Examples:**
```
# In Slack channel
@Devin Use the "PR Review" skill on #pull-requests

# Direct message
/Devin Run "Bug Triage" skill on issue #1234
```

### GitHub Integration

**Automatic Triggers:**
```yaml
# .github/workflows/devin-pr-review.yml
name: Devin PR Review
on:
  pull_request:
    types: [opened, synchronize]

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: cognition-ai/devin-action@v1
        with:
          skill: "pr-review-checklist"
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

### Jira/Linear Integration

**Workflow:**
```
1. Create ticket in Jira/Linear
2. Add label: "devin-eligible"
3. Devin automatically picks up ticket
4. Runs appropriate skill based on ticket type
5. Updates ticket with progress
6. Creates PR when complete
```

---

## 💡 Part 5: Best Practices from Coding Agents 101

### 1. Say HOW, Not Just WHAT

**Bad Prompt:**
```
"Add unit tests"
```

**Good Prompt:**
```
"Add unit tests for the payment module. Focus on:
- Testing all public methods in PaymentService
- Edge cases: invalid cards, expired cards, insufficient funds
- Mock the Stripe API using jest.mock()
- Target 85% code coverage
- Follow existing test patterns in tests/payment/"
```

### 2. Tell Devin Where to Start

**Bad:**
```
"Fix the search bug"
```

**Good:**
```
"Fix the search bug. Start by looking at:
- src/search/search_controller.py (main logic)
- tests/test_search.py (failing tests)
- The error occurs when searching with special characters
- Check the regex pattern on line 47"
```

### 3. Practice Defensive Prompting

Anticipate where Devin might go wrong:

```
"Please refactor the authentication module. Important notes:
- DO NOT change the public API surface
- Keep backward compatibility with existing clients
- Run all auth tests after each major change
- The token validation logic is critical - add extra tests"
```

### 4. Set Checkpoints for Large Tasks

```
"I want you to migrate our codebase from JavaScript to TypeScript.

Step 1: Set up TypeScript configuration (tsconfig.json, types)
→ STOP and show me the config before proceeding

Step 2: Convert utility functions (src/utils/)
→ Run tests, verify no type errors

Step 3: Convert API layer (src/api/)
→ Update function signatures with types

Step 4: Convert React components
→ Fix any remaining type errors

After each step, wait for my approval before continuing."
```

### 5. Teach Verification

Don't just say "it's broken" - explain HOW to verify:

```
"When you finish the feature, verify it works by:
1. Running: npm run test:integration
2. Starting the dev server: npm run dev
3. Navigating to /settings/profile
4. Uploading a test image (use test-image.jpg)
5. Confirming the image displays correctly
6. Checking the network tab for API errors"
```

---

## 📊 Part 6: Skill Library - Ready-to-Use Templates

### Template 1: PR Review Skill

```markdown
# PR Review Checklist

## Objective
Review pull requests for code quality, security, and best practices.

## Steps
1. Read PR description and linked issue
2. Review changed files (focus on business logic)
3. Check for:
   - Security vulnerabilities (SQL injection, XSS, auth bypass)
   - Performance issues (N+1 queries, unbounded loops)
   - Code style consistency
   - Test coverage
   - Error handling
4. Leave constructive comments
5. Approve or request changes

## Forbidden
- Never approve without reviewing tests
- Never ignore security concerns
- Never approve if CI is failing
```

### Template 2: Bug Fix Skill

```markdown
# Bug Fix Workflow

## Objective
Diagnose and fix bugs with proper testing and documentation.

## Steps
1. **Reproduce**
   - Read bug report carefully
   - Reproduce the issue locally
   - Document reproduction steps

2. **Diagnose**
   - Check logs and error messages
   - Use debugger to trace execution
   - Identify root cause (not just symptoms)

3. **Fix**
   - Implement minimal fix
   - Avoid unrelated refactoring
   - Add regression test

4. **Validate**
   - Run full test suite
   - Verify fix in staging environment
   - Check for side effects

5. **Document**
   - Update bug report with solution
   - Add to known issues if relevant
   - Commit with clear message referencing issue

## Required from User
- Bug report or error description
- Steps to reproduce (if available)
- Expected vs actual behavior
```

### Template 3: Feature Implementation Skill

```markdown
# Feature Implementation

## Objective
Implement new features from specification to production-ready code.

## Steps
1. **Understand Requirements**
   - Read PRD/specification document
   - Clarify ambiguous requirements with user
   - Identify dependencies and constraints

2. **Design**
   - Create technical design doc
   - Define API contracts (if applicable)
   - Plan database changes
   - Identify testing strategy

3. **Implement**
   - Set up feature branch
   - Implement backend logic
   - Implement frontend (if applicable)
   - Add comprehensive tests

4. **Test**
   - Unit tests (80%+ coverage)
   - Integration tests
   - Manual testing checklist
   - Performance testing (if applicable)

5. **Deploy**
   - Create PR with detailed description
   - Update documentation
   - Add feature flag (if applicable)
   - Monitor after deployment

## Specifications
- Follow existing code style
- Use feature flags for gradual rollout
- Include error handling and logging
- Update API documentation

## Required from User
- Feature specification or PRD
- Design mockups (if UI feature)
- Acceptance criteria
- Target release date
```

---

## 🚀 Part 7: Measuring Skill Effectiveness

### Key Metrics to Track

| Metric | How to Measure | Target |
|--------|----------------|--------|
| **Success Rate** | % of tasks completed without human intervention | 80%+ |
| **Time Saved** | Hours saved per task vs manual | 60%+ reduction |
| **Quality Score** | Code review passes on first try | 70%+ |
| **Coverage** | Test coverage of generated code | 80%+ |
| **User Satisfaction** | Team feedback scores | 4/5+ |

### Continuous Improvement Loop

```
1. Run skill on real task
       ↓
2. Review output quality
       ↓
3. Identify gaps or errors
       ↓
4. Update skill with learnings
       ↓
5. Test updated skill
       ↓
6. Share improvements with team
```

---

## ⚠️ Part 8: Common Mistakes and How to Avoid Them

### Mistake 1: Vague Objectives

**Bad:**
```
"Improve the code"
```

**Good:**
```
"Refactor the user authentication module to:
- Extract password validation into separate utility
- Add rate limiting for login attempts
- Implement JWT token refresh mechanism
- Maintain backward compatibility with existing API"
```

### Mistake 2: Missing Context

**Bad:**
```
"Fix the bug in checkout"
```

**Good:**
```
"Fix the checkout bug where users see 'Payment Failed' even with valid cards.
- Issue started after Stripe SDK update to v3.2.1
- Error logs show: 'Invalid API key format'
- Affected files: src/checkout/payment_processor.py
- Test card 4242 4242 4242 4242 reproduces the issue"
```

### Mistake 3: No Verification Steps

**Bad:**
```
"Add the new feature and test it"
```

**Good:**
```
"Add the new export feature. Verify by:
1. Running: npm run test:unit
2. Starting dev server
3. Going to /reports
4. Clicking 'Export CSV'
5. Confirming file downloads with correct data
6. Checking browser console for errors"
```

### Mistake 4: Skipping Forbidden Actions

Always specify what NOT to do:

```markdown
## Forbidden Actions
- Do NOT modify database schema without approval
- Do NOT deploy to production directly
- Do NOT commit API keys or secrets
- Do NOT skip running tests
- Do NOT change public API without versioning
```

### Mistake 5: Not Iterating

Skills should evolve:
- After each use, note what worked/didn't
- Update skill monthly based on learnings
- Share improvements with team
- Version your skills (v1.0, v1.1, v2.0)

---

## 🎓 Part 9: Learning Path - From Beginner to Expert

### Week 1-2: Basics
- [ ] Set up Devin access and connect repos
- [ ] Run 5 simple tasks (fix typos, add comments)
- [ ] Create your first skill (simple, repetitive task)
- [ ] Test skill 3 times, refine based on results

### Week 3-4: Intermediate
- [ ] Create 3 skills for common team workflows
- [ ] Integrate Devin with Slack/GitHub
- [ ] Handle multi-file changes
- [ ] Implement checkpoint-based skills

### Week 5-8: Advanced
- [ ] Create skills with external tool integration (MCPs)
- [ ] Implement conditional logic in skills
- [ ] Set up automatic triggers (webhooks)
- [ ] Train team on using skills

### Week 9+: Expert
- [ ] Build skill library for organization
- [ ] Measure and optimize skill performance
- [ ] Contribute skills to community
- [ ] Mentor others on skill creation

---

## 📖 Part 10: Resources and Further Reading

### Official Documentation
- [Devin Docs](https://docs.devin.ai/)
- [Coding Agents 101](https://devin.ai/agents101)
- [API Reference](https://docs.devin.ai/api-reference/overview)

### Community Resources
- [Devin Community Slack](https://app.devin.ai/settings/support)
- [Skill Templates Gallery](https://devin.ai/community/playbooks)
- [Best Practices Forum](https://community.cognition.ai/)

### Related Tools
- **MCP Directory**: Model Context Protocols for external integrations
- **DeepWiki**: Codebase search and understanding
- **Codium**: AI-powered test generation

---

## 🎯 Quick Reference Card

### Before Creating a Skill
```
□ Is this task repetitive?
□ Can I document clear steps?
□ Are success criteria measurable?
□ Will others benefit from this?
```

### Skill Structure Checklist
```
□ Clear objective statement
□ Step-by-step instructions
□ Specifications and quality standards
□ Forbidden actions
□ Required inputs from user
□ Verification steps
□ Common pitfalls and advice
```

### Testing Your Skill
```
□ Test with simple task first
□ Review output quality
□ Test with edge cases
□ Get feedback from teammates
□ Iterate and improve
```

---

**Last Updated:** April 13, 2026  
**Author:** weisenaibot 🐺  
**License:** Internal use only
