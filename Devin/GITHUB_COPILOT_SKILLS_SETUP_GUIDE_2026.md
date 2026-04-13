# GitHub Copilot Skills: Complete Setup Guide 2026

**Created:** April 13, 2026  
**Version:** 1.0  
**Sources:** Official GitHub Docs + VS Code Docs + Agent Skills Specification + Industry Best Practices

---

## 🎯 Executive Summary

**GitHub Copilot Agent Skills** are reusable, portable instruction packages that teach Copilot specialized workflows and procedures. Skills work across VS Code, GitHub Copilot CLI, and GitHub Copilot cloud agent using an open standard ([agentskills.io](https://agentskills.io)).

**Key Benefits:**
- ✅ **Specialize Copilot** - Domain-specific capabilities without repeating context
- ✅ **Reduce Repetition** - Create once, use automatically across all conversations
- ✅ **Compose Capabilities** - Combine multiple skills for complex workflows
- ✅ **Efficient Loading** - Only relevant skills load into context (Progressive Disclosure)
- ✅ **Cross-Tool Compatibility** - Works with 30+ AI agents (Copilot, Claude Code, Codex, Cursor, etc.)

**Skill Locations:**
| Scope | Location | Use Case |
|-------|----------|----------|
| **Project** | `.github/skills/`, `.claude/skills/`, `.agents/skills/` | Repository-specific workflows |
| **User (Global)** | `~/.copilot/skills/`, `~/.claude/skills/`, `~/.agents/skills/` | Personal workflows across all projects |

---

## 📋 Part 1: Understanding Agent Skills

### What Are Agent Skills?

**Definition:** Agent Skills are folders containing instructions (`SKILL.md`), scripts, examples, and resources that AI coding agents can load when relevant to perform specialized tasks.

**Key Characteristics:**
- **Open Standard** - Defined by [agentskills.io](https://agentskills.io), supported by 30+ tools
- **Task-Specific** - Loaded on-demand based on relevance (not always-on like custom instructions)
- **Portable** - Works across VS Code, Copilot CLI, Copilot cloud agent, Claude Code, Cursor, etc.
- **Resource-Rich** - Can include scripts, templates, examples alongside instructions

### Skills vs Custom Instructions

| Aspect | Agent Skills | Custom Instructions |
|--------|--------------|---------------------|
| **Purpose** | Specialized workflows & procedures | Coding standards & conventions |
| **Loading** | On-demand (when relevant) | Always applied (or path-based) |
| **Content** | Instructions + scripts + examples + resources | Instructions only |
| **Portability** | Open standard (cross-tool) | VS Code or GitHub specific |
| **Scope** | Per task/topic | Per file path or entire repo |
| **File Format** | `SKILL.md` with YAML frontmatter | `.instructions.md`, `copilot-instructions.md` |

**When to Use Skills:**
- ✅ Creating reusable capabilities across different AI tools
- ✅ Including scripts, examples, or resources alongside instructions
- ✅ Sharing capabilities with the wider AI community
- ✅ Defining specialized workflows (testing, debugging, deployment)

**When to Use Custom Instructions:**
- ✅ Defining project-specific coding standards
- ✅ Setting language or framework conventions
- ✅ Specifying code review or commit message guidelines
- ✅ Applying rules based on file types using glob patterns

---

## 🏗️ Part 2: SKILL.md File Format

### Structure Overview

```markdown
---
name: skill-name
description: Description of what the skill does and when to use it
argument-hint: [optional hint text]
user-invocable: true
disable-model-invocation: false
license: MIT
metadata:
  author: dev-team
  version: "1.0"
---

# Skill Instructions

Your detailed instructions, guidelines, and examples go here...
```

### YAML Frontmatter Fields

| Field | Required | Description | Default |
|-------|----------|-------------|---------|
| `name` | **Yes** | Unique identifier. Lowercase with hyphens, max 64 chars. Must match directory name. | - |
| `description` | **Yes** | What the skill does and when to use it. Max 1024 chars. Include trigger keywords! | - |
| `argument-hint` | No | Hint text shown in chat input when invoked as slash command | - |
| `user-invocable` | No | Show as slash command in `/` menu | `true` |
| `disable-model-invocation` | No | Auto-load based on relevance | `false` |
| `license` | No | License (MIT, Apache-2.0, etc.) | - |
| `metadata` | No | Supplementary info (author, version, etc.) | - |
| `allowed-tools` | No | Pre-approved tools (shell, bash) - use cautiously! | - |

### Description Best Practices (Critical!)

**The description determines 80% of activation accuracy.** Include trigger keywords explicitly.

```yaml
# ❌ Bad - Too vague
description: Helps with testing

# ✅ Good - Specific with trigger keywords
description: >-
  Assists with web application test strategies and automated test creation.
  Use for topics related to testing, test, E2E, unit testing, and integration test.

# ✅ Good - Clear use cases
description: >-
  Guide for debugging failing GitHub Actions workflows.
  Use when asked to debug CI/CD, workflow failures, build errors, or PR checks.
```

### Slash Command Configuration

| Configuration | Slash Command (`/`) | Auto-Loaded by Model | Use Case |
|---------------|---------------------|----------------------|----------|
| Default (both omitted) | ✅ Yes | ✅ Yes | General-purpose skills |
| `user-invocable: false` | ❌ No | ✅ Yes | Background knowledge (model loads when relevant) |
| `disable-model-invocation: true` | ✅ Yes | ❌ No | On-demand only skills |
| Both set | ❌ No | ❌ No | Disabled skills |

---

## 🛠️ Part 3: Step-by-Step Setup

### Step 1: Enable Agent Skills (VS Code)

**Prerequisites:**
- GitHub Copilot extension installed
- Active Copilot subscription (Free, Pro, or Enterprise)
- Agent Skills preview enabled

**Enable in VS Code:**
1. Open VS Code Settings (`Ctrl+,` or `Cmd+,`)
2. Search for `chat.useAgentSkills`
3. Check the box to enable
4. Or add to `settings.json`:

```json
{
  "chat.useAgentSkills": true
}
```

**Configure Skill Locations (Optional):**
```json
{
  "chat.agentSkillsLocations": {
    ".github/skills/**": true,
    ".agents/skills/**": true,
    ".claude/skills/**": true
  }
}
```

**Verify Configuration:**
1. Open Chat view in VS Code
2. Type `/skills` in chat input
3. Select "Configure Skills" from menu
4. Verify your skills appear in the list

---

### Step 2: Create Project-Level Skills

**Directory Structure:**
```
your-repository/
├── .github/
│   └── skills/
│       ├── webapp-testing/
│       │   ├── SKILL.md
│       │   ├── test-template.js
│       │   └── naming-conventions.md
│       ├── github-actions-debugging/
│       │   └── SKILL.md
│       └── api-documentation/
│           ├── SKILL.md
│           └── docs-template.md
├── src/
└── README.md
```

**Create Skill Directory:**
```bash
# Navigate to your repository
cd /path/to/your/repo

# Create skills directory (choose one location)
mkdir -p .github/skills/webapp-testing

# Or for Claude Code compatibility
mkdir -p .claude/skills/webapp-testing

# Or for generic agent compatibility
mkdir -p .agents/skills/webapp-testing
```

**Create SKILL.md File:**
```bash
cat > .github/skills/webapp-testing/SKILL.md << 'EOF'
---
name: webapp-testing
description: >-
  Assists with web application test strategies and automated test creation.
  Use for topics related to testing, test, E2E, unit testing, and integration test.
license: MIT
metadata:
  author: dev-team
  version: "1.0"
---

# Web Application Testing with Playwright

This skill helps you create and run browser-based tests for web applications using Playwright.

## When to Use This Skill

Use this skill when you need to:
- Create new Playwright tests for web applications
- Debug failing browser tests
- Set up test infrastructure for a new project

## Creating Tests

1. Review the [test template](./test-template.js) for the standard test structure
2. Identify the user flow to test
3. Create a new test file in the `tests/` directory
4. Use Playwright's locators to find elements (prefer role-based selectors)
5. Add assertions to verify expected behavior

## Running Tests

To run tests locally:
```bash
npx playwright test
```

To debug tests:
```bash
npx playwright test --debug
```

## Best Practices

- Use data-testid attributes for dynamic content
- Keep tests independent and atomic
- Use Page Object Model for complex pages
- Take screenshots on failure
EOF
```

**Add Supporting Resources:**
```bash
# Create test template
cat > .github/skills/webapp-testing/test-template.js << 'EOF'
// Test Template - AAA Pattern (Arrange-Act-Assert)

import { test, expect } from '@playwright/test';

test.describe('Feature Name', () => {
  test('should expected behavior', async ({ page }) => {
    // Arrange
    await page.goto('/target-page');
    
    // Act
    await page.click('[data-testid="action-button"]');
    
    // Assert
    await expect(page.locator('[data-testid="result"]')).toBeVisible();
  });
});
EOF
```

---

### Step 3: Create User-Level (Global) Skills

**Directory Locations:**
```bash
# For GitHub Copilot (all projects)
mkdir -p ~/.copilot/skills

# For Claude Code compatibility
mkdir -p ~/.claude/skills

# For generic agent compatibility  
mkdir -p ~/.agents/skills
```

**Example: GitHub CLI Skill (Global):**
```bash
cat > ~/.copilot/skills/github-cli/SKILL.md << 'EOF'
---
name: github-cli
description: >-
  Guide for using GitHub CLI (gh) for common operations.
  Use when asked to create PRs, manage issues, check CI status, or interact with GitHub.
allowed-tools: shell
---

# GitHub CLI Operations

This skill provides instructions for common GitHub CLI operations.

## Creating a Pull Request

```bash
# Create branch and push
git checkout -b feature/your-feature
git add .
git commit -m "feat: your commit message"
git push -u origin HEAD

# Create PR
gh pr create \
  --title "feat: your feature" \
  --body "Description of changes" \
  --base main \
  --label "enhancement"
```

## Checking CI Status

```bash
# List recent workflow runs
gh run list --limit 5

# View specific run
gh run view <run-id>

# Watch run in real-time
gh run watch <run-id>
```

## Managing Issues

```bash
# Create issue
gh issue create --title "Bug: description" --body "Steps to reproduce"

# List issues
gh issue list --state open

# Add comment
gh issue comment <issue-number> --body "Your comment"
```

## Reviewing PRs

```bash
# List PRs
gh pr list

# Checkout PR locally
gh pr checkout <pr-number>

# Review and approve
gh pr review <pr-number> --approve
gh pr review <pr-number> --comment --body "Feedback"
```
EOF
```

**Important Security Note:**
> ⚠️ **WARNING:** Only pre-approve `shell` or `bash` tools if you have reviewed the skill and fully trust its source. Pre-approving removes the confirmation step and can allow arbitrary command execution. When in doubt, omit `allowed-tools` so Copilot asks for explicit confirmation.

---

### Step 4: Test Your Skills

**Method 1: Slash Command Invocation**
```
1. Open VS Code Chat
2. Type: /webapp-testing for the login page
3. Copilot loads the skill and follows instructions
```

**Method 2: Natural Language Trigger**
```
1. Ask: "Help me create tests for the auth module"
2. Copilot matches your query to skill descriptions
3. Relevant skills auto-load based on description keywords
```

**Method 3: Verify Skill Loading**
```
1. Type /skills in chat
2. Select "Configure Skills"
3. See list of available skills
4. Toggle skills on/off as needed
```

**Test Checklist:**
```
□ Skill appears in /skills menu
□ Skill description triggers correctly
□ Instructions load into context
✓ Referenced resources (scripts, templates) accessible
□ Skill produces expected output
```

---

## 📚 Part 4: Skill Templates

### Template 1: Test Automation Skill

```markdown
---
name: test-automation
description: >-
  Creates comprehensive unit and integration tests following project conventions.
  Use for testing, unit tests, integration tests, test coverage, TDD.
argument-hint: "[file or module to test]"
license: MIT
metadata:
  author: engineering-team
  version: "1.0"
---

# Test Automation Skill

## Goal
Improve test coverage and standardize test quality across the codebase.

## Testing Strategy

### Unit Tests
- **Focus**: Business logic, edge cases, boundary values
- **Pattern**: AAA (Arrange-Act-Assert)
- **Coverage Target**: 80%+ for new code

### Integration Tests
- **Focus**: API endpoints, database interactions, external services
- **Pattern**: Given-When-Then
- **Coverage Target**: Critical paths only

### E2E Tests
- **Focus**: User flows, critical journeys
- **Pattern**: User story format
- **Coverage Target**: Happy path + key error scenarios

## Test File Conventions

- **Naming**: `*.test.ts` or `*.spec.ts`
- **Location**: Mirror source structure in `tests/` directory
- **Describe blocks**: `describe('Feature Name', () => {...})`
- **Test names**: `it('should expected behavior', () => {...})`

## Process

1. **Analyze Target Code**
   - Identify all public functions/classes
   - Note external dependencies (mock these)
   - Identify edge cases and boundary conditions

2. **Create Test Structure**
   - Use [test template](./test-template.js) as starting point
   - Follow naming conventions from [naming-guide.md](./naming-guide.md)
   - Set up fixtures and mocks

3. **Write Tests**
   - Happy path first
   - Edge cases (null, empty, boundaries)
   - Error handling scenarios
   - Mock all external dependencies

4. **Validate**
   - Run: `npm run test`
   - Check coverage: `npm run test:coverage`
   - Fix any failing tests
   - Ensure no flaky tests

## References
- [Test Template](./test-template.js)
- [Naming Conventions](./naming-guide.md)
- [Mocking Guide](./mocking-guide.md)
```

---

### Template 2: CI/CD Debugging Skill

```markdown
---
name: ci-cd-debugging
description: >-
  Debugs failing CI/CD pipelines, GitHub Actions, and build processes.
  Use for CI failures, build errors, workflow issues, deployment problems.
allowed-tools: shell
---

# CI/CD Debugging Skill

## When to Use
- GitHub Actions workflow failing
- Build process errors
- Deployment pipeline issues
- Test suite failures in CI

## Debugging Process

### Step 1: Gather Information
```bash
# List recent workflow runs
gh run list --limit 10

# Get details of failed run
gh run view <run-id>

# Download logs
gh run download <run-id>
```

### Step 2: Analyze Failure
1. Check which job/step failed
2. Review error messages in logs
3. Identify if it's:
   - Dependency issue (missing package, version conflict)
   - Configuration issue (secrets, environment variables)
   - Code issue (test failure, compilation error)
   - Infrastructure issue (timeout, resource limits)

### Step 3: Reproduce Locally
```bash
# Run same commands as CI
npm ci
npm run build
npm run test

# Use act to run GitHub Actions locally
act -j <job-name>
```

### Step 4: Fix and Verify
1. Implement fix based on root cause
2. Test locally
3. Push changes
4. Monitor CI run

## Common Issues & Solutions

### Missing Dependencies
```yaml
# Add to workflow
- run: npm ci
  env:
    NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

### Timeout Issues
```yaml
# Increase timeout
timeout-minutes: 30

# Or split into smaller jobs
```

### Secret Configuration
```yaml
# Ensure secrets are set in repo settings
# Settings > Secrets and variables > Actions
```

## Tools
- GitHub CLI (`gh`)
- `act` for local Actions testing
- Repository workflow logs
```

---

### Template 3: API Documentation Skill

```markdown
---
name: api-documentation
description: >-
  Generates and maintains API documentation from code comments and OpenAPI specs.
  Use for API docs, OpenAPI, Swagger, documentation generation.
---

# API Documentation Skill

## Goal
Maintain up-to-date, comprehensive API documentation that syncs with code.

## Documentation Standards

### OpenAPI Specification
- All endpoints documented in `openapi.yaml`
- Request/response schemas defined
- Authentication methods specified
- Error responses documented

### Code Comments
- JSDoc/TSDoc for all public functions
- Parameter descriptions
- Return value documentation
- Example usage

## Generation Process

### For New Endpoints

1. **Add OpenAPI Definition**
   ```yaml
   /api/users/{id}:
     get:
       summary: Get user by ID
       parameters:
         - name: id
           in: path
           required: true
           schema:
             type: string
       responses:
         '200':
           description: User object
   ```

2. **Add Code Comments**
   ```typescript
   /**
    * Get user by ID
    * @param id - User identifier
    * @returns User object
    * @throws 404 if user not found
    */
   async getUser(id: string): Promise<User> { ... }
   ```

3. **Generate Docs**
   ```bash
   npm run docs:generate
   ```

4. **Verify Output**
   - Check generated docs for accuracy
   - Test example requests
   - Verify all endpoints covered

### For Documentation Updates

1. Run doc generation
2. Compare with previous version
3. Update changelog
4. Deploy to docs site

## Tools
- [docs-template.md](./docs-template.md) - Documentation structure
- `npm run docs:generate` - Generation script
- `npm run docs:serve` - Local preview

## Quality Checks
- All public endpoints documented
- Examples are functional
- Error cases covered
- Authentication requirements clear
```

---

### Template 4: Security Review Skill

```markdown
---
name: security-review
description: >-
  Performs security code review focusing on common vulnerabilities.
  Use for security audit, vulnerability check, code review, pre-deployment.
---

# Security Review Skill

## Objective
Identify and remediate security vulnerabilities before deployment.

## Review Checklist

### Authentication & Authorization
- [ ] All endpoints require authentication
- [ ] Role-based access control implemented
- [ ] Session management secure
- [ ] No hardcoded credentials

### Input Validation
- [ ] All user inputs validated
- [ ] SQL injection prevented (parameterized queries)
- [ ] XSS prevented (output encoding)
- [ ] CSRF tokens implemented

### Data Protection
- [ ] Sensitive data encrypted at rest
- [ ] TLS for data in transit
- [ ] No sensitive data in logs
- [ ] Proper secret management (not in code)

### Common Vulnerabilities
- [ ] No eval() or unsafe deserialization
- [ ] Rate limiting on sensitive endpoints
- [ ] Security headers configured
- [ ] Dependencies up to date (no known CVEs)

## Review Process

1. **Automated Scan**
   ```bash
   npm audit
   npm run security:scan
   ```

2. **Manual Review**
   - Review auth flows
   - Check input validation
   - Verify error handling (no info leakage)

3. **Document Findings**
   - Log all issues found
   - Prioritize by severity
   - Create remediation tickets

4. **Verify Fixes**
   - Re-scan after fixes
   - Confirm no regressions

## Tools
- `npm audit` - Dependency vulnerabilities
- `npm run security:scan` - Static analysis
- [security-checklist.md](./security-checklist.md) - Detailed checklist

## Severity Levels
- **Critical**: Immediate fix required (auth bypass, data exposure)
- **High**: Fix before deployment (XSS, SQL injection)
- **Medium**: Fix in next sprint (missing headers, weak validation)
- **Low**: Address in backlog (minor issues, improvements)
```

---

## 🔗 Part 5: Installing Third-Party Skills

### Official Skill Repositories

**Awesome Copilot (GitHub Official):**
```bash
# List available skills
copilot plugin list

# Install a skill/plugin
copilot plugin install <plugin-name>@awesome-copilot

# Example: Install GitHub CLI skills
copilot plugin install github-cli@awesome-copilot
```

**Vercel Skills Manager:**
```bash
# Install skills from GitHub repo
npx skills add Arize-ai/arize-skills

# Interactive selection (choose skills, agent, scope)
npx skills add

# Install from specific branch/tag
npx skills add owner/repo --branch main
```

### Manual Installation

**From GitHub Repository:**
```bash
# Clone skill repo
git clone https://github.com/owner/skill-repo.git /tmp/skills

# Copy to project skills
cp -r /tmp/skills/skill-name .github/skills/

# Or copy to global skills
cp -r /tmp/skills/skill-name ~/.copilot/skills/
```

**Skill Discovery:**
- [github/awesome-copilot](https://github.com/github/awesome-copilot)
- [agentskills.io directory](https://agentskills.io)
- Search GitHub for `SKILL.md` files

---

## 💡 Part 6: Best Practices

### Skill Design Principles

**1. Fine-Grained, Specialized Skills**
```
✅ Good: Separate skills for "unit-testing", "e2e-testing", "integration-testing"
❌ Bad: One giant "testing" skill covering everything

Why: Only 1-3 skills load per task. Fine-grained skills = better relevance matching.
```

**2. Clear Trigger Keywords in Description**
```
✅ Good: "Use for testing, test, E2E, unit testing, integration test, Jest, Playwright"
❌ Bad: "Helps with tests"

Why: Description matching determines 80% of activation accuracy.
```

**3. Progressive Disclosure**
```
✅ Good: Reference external files, don't inline everything
❌ Bad: Put all content in SKILL.md

Why: Resources only load when referenced, keeping context efficient.
```

**4. Include Examples**
```
✅ Good: Show expected input/output, code examples
❌ Bad: Only abstract instructions

Why: Examples reduce ambiguity and improve output quality.
```

**5. Test and Iterate**
```
1. Create skill
2. Test with real queries
3. Check if it triggers correctly
4. Refine description if needed
5. Update instructions based on results
```

---

### Skill Organization

**Project Structure:**
```
.github/skills/
├── testing/
│   ├── unit-testing/
│   ├── integration-testing/
│   └── e2e-testing/
├── documentation/
│   ├── api-docs/
│   └── readme-generator/
├── ci-cd/
│   ├── github-actions/
│   └── deployment/
└── security/
    ├── code-review/
    └── vulnerability-scan/
```

**Naming Conventions:**
- Lowercase with hyphens: `unit-testing` not `UnitTesting`
- Match directory name: `name: webapp-testing` in `webapp-testing/SKILL.md`
- Descriptive but concise: max 64 characters

---

### Context Efficiency

**Progressive Disclosure in Action:**

```
Level 1: Discovery (Always loaded)
└─ Reads: name + description from YAML frontmatter
   Size: ~200 tokens per skill

Level 2: Instructions (Loaded when triggered)
└─ Reads: SKILL.md body
   Size: ~500-2000 tokens per skill

Level 3: Resources (Loaded when referenced)
└─ Reads: Scripts, templates, examples
   Size: Variable, only when needed

Result: 30 skills installed ≈ 6,000 tokens potential
        Actual per task ≈ 1-3 skills loaded ≈ 500-2,000 tokens
```

**Guidelines:**
- Install 10-30 skills per project (manageable)
- Each skill focused on one task
- Only 1-3 skills actually load per conversation
- Reference external files for large content

---

### Security Considerations

**Pre-Approving Tools:**
```yaml
# ⚠️ DANGEROUS - Only if you fully trust the skill
allowed-tools: shell

# ✅ SAFER - Let Copilot ask for confirmation
# (omit allowed-tools field)
```

**Best Practices:**
1. Review any skill before installing (especially from third parties)
2. Don't pre-approve shell access unless necessary
3. Keep global skills minimal and trusted
4. Audit project skills in code review
5. Use version control for skills (they're code!)

---

## 📊 Part 7: Metrics and Optimization

### Skill Effectiveness Metrics

| Metric | How to Measure | Target |
|--------|----------------|--------|
| **Activation Accuracy** | % of times skill loads when relevant | 80%+ |
| **Task Success Rate** | % of tasks completed successfully with skill | 70%+ |
| **Context Efficiency** | Tokens used vs. tasks completed | Decreasing |
| **User Satisfaction** | Developer feedback scores | 4/5+ |
| **Reuse Frequency** | Times skill invoked per week | Increasing |

### Continuous Improvement

```
1. Deploy skill
     ↓
2. Monitor usage (which skills trigger, which don't)
     ↓
3. Collect feedback (does it help?)
     ↓
4. Analyze failures (why didn't it work?)
     ↓
5. Update description/instructions
     ↓
6. Version and redeploy
```

---

## 🎓 Part 8: Learning Path

### Week 1: Basics
- [ ] Enable Agent Skills in VS Code
- [ ] Create first simple skill (e.g., project-specific greeting)
- [ ] Test skill with slash command
- [ ] Read official GitHub docs on skills

### Week 2-3: Practical Skills
- [ ] Create 3 project-specific skills (testing, docs, CI/CD)
- [ ] Add supporting resources (templates, scripts)
- [ ] Test with natural language triggers
- [ ] Share skills with team

### Week 4-6: Advanced
- [ ] Create global skills for common tools
- [ ] Install third-party skills
- [ ] Optimize skill descriptions for better triggering
- [ ] Build skill library for organization

### Week 7+: Expert
- [ ] Contribute skills to awesome-copilot
- [ ] Create skills for your product/service
- [ ] Train team on skill creation
- [ ] Establish skill governance process

---

## 📖 Part 9: Resources

### Official Documentation
- [GitHub Docs: Creating Agent Skills](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/create-skills)
- [VS Code: Agent Skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills)
- [Agent Skills Specification](https://agentskills.io)
- [Awesome Copilot](https://github.com/github/awesome-copilot)

### Tools
- **Vercel Skills Manager**: `npx skills add`
- **Copilot CLI**: `copilot plugin install`
- **Chat Customizations Editor**: `/skills` in VS Code

### Community
- [GitHub Copilot Community](https://github.com/community/copilot)
- [Agent Skills Directory](https://agentskills.io/directory)
- [r/GithubCopilot](https://reddit.com/r/GithubCopilot)

---

## 🎯 Quick Reference

### Before Creating a Skill
```
□ Is this task repetitive enough to justify a skill?
□ Can I write clear, specific instructions?
□ Are there trigger keywords for the description?
□ Will others benefit from this skill?
```

### Skill Checklist
```
□ YAML frontmatter complete (name, description required)
□ Description includes trigger keywords
□ Instructions are specific and actionable
□ Examples provided
□ Resources referenced with relative paths
□ Skill tested with slash command and natural language
```

### Troubleshooting
```
Skill not appearing in / menu:
→ Check name matches directory
→ Verify user-invocable: true (or omit)
→ Restart VS Code

Skill not auto-loading:
→ Add more trigger keywords to description
→ Check disable-model-invocation: false
→ Ensure query matches description

Skill not working correctly:
→ Review instructions for clarity
→ Add more examples
→ Check referenced files exist
```

---

## 📤 Part 10: Pushing Skills Report to GitHub

### Create Summary Document

After setting up skills, create a summary for your team:

```markdown
# Copilot Skills Inventory

## Project Skills (.github/skills/)

| Skill | Purpose | Status |
|-------|---------|--------|
| webapp-testing | Playwright test automation | ✅ Active |
| ci-cd-debugging | GitHub Actions debugging | ✅ Active |
| api-documentation | OpenAPI doc generation | 🚧 WIP |

## Global Skills (~/.copilot/skills/)

| Skill | Purpose | Status |
|-------|---------|--------|
| github-cli | GitHub CLI operations | ✅ Active |
| security-review | Security code review | ✅ Active |

## Usage Guidelines

1. Type `/skills` to see available skills
2. Skills auto-load based on your query
3. Use slash commands for explicit invocation
4. Report issues or request new skills in #copilot channel
```

### Push to Dropbox Repository

```bash
# Create skills report
cat > GITHUB_COPILOT_SKILLS_INVENTORY.md << 'EOF'
# GitHub Copilot Skills Inventory

[Your skills summary here]
EOF

# Commit to dropbox repo
cd /path/to/dropbox-repo
git add Devin/GITHUB_COPILOT_SKILLS_SETUP_GUIDE_2026.md
git add GITHUB_COPILOT_SKILLS_INVENTORY.md
git commit -m "Add: GitHub Copilot Skills setup guide and inventory"
git push origin main
```

---

**Last Updated:** April 13, 2026  
**Author:** weisenaibot 🐺  
**License:** Internal use only  
**Based on:** Official GitHub Docs + VS Code Docs + Agent Skills Specification
