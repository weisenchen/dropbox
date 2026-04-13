# Devin Managed Devins: Coordinator-Worker Architecture Guide 2026

**Created:** April 13, 2026  
**Version:** 1.0  
**Sources:** Official Cognition AI Blog + Devin Docs + Nubank Case Study + Industry Research

---

## 🎯 Executive Summary

**Managed Devins** (also known as **Coordinator-Worker Architecture**) is Devin's most powerful feature for tackling large-scale, long-running engineering tasks. Instead of one agent working sequentially, a **coordinator Devin** orchestrates multiple **worker Devins** running in parallel, each in its own isolated VM.

**Key Announcement (March 19, 2026):**
> "Devin can now break down large tasks and delegate them to a team of managed Devins, with each running in its own isolated VM in parallel."
> — Cognition AI Team

**Real-World Results (Nubank Case Study):**
- **8-12x** engineering time efficiency gain
- **20x** cost savings
- **40 min → 10 min** per sub-task after fine-tuning
- **100,000+** data class migrations completed in weeks vs. 18 months

---

## 📋 Part 1: Understanding Coordinator-Worker Architecture

### What Are Managed Devins?

**Definition:** Managed Devins are full Devin instances that a coordinator Devin can spawn, delegate tasks to, and merge results from. Each managed Devin runs in its own isolated virtual machine with:
- Dedicated shell access
- Independent code editor
- Separate browser session
- Isolated file system

**The Coordinator-Worker Pattern:**

```
┌─────────────────────────────────────────────────────────────────┐
│                    COORDINATOR DEVIN                             │
│  (Main Session - "Engineering Manager")                         │
│                                                                  │
│  Responsibilities:                                               │
│  • Task decomposition                                            │
│  • Worker assignment                                             │
│  • Progress tracking                                             │
│  • Quality control                                               │
│  • Result merging                                                │
│  • Error handling & retry                                        │
└─────────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
┌───────────────┐   ┌───────────────┐   ┌───────────────┐
│  WORKER 1     │   │  WORKER 2     │   │  WORKER 3     │
│  (Specialist) │   │  (Specialist) │   │  (Specialist) │
│               │   │               │   │               │
│ • Isolated VM │   │ • Isolated VM │   │ • Isolated VM │
│ • Own shell   │   │ • Own shell   │   │ • Own shell   │
│ • Own browser │   │ • Own browser │   │ • Own browser │
│ • Parallel    │   │ • Parallel    │   │ • Parallel    │
└───────────────┘   └───────────────┘   └───────────────┘
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              ▼
                    ┌───────────────────┐
                    │   MERGE & REVIEW  │
                    │   (Coordinator)   │
                    └───────────────────┘
```

### When to Use Managed Devins

**✅ Ideal Use Cases:**

| Task Type | Why It Works | Example |
|-----------|--------------|---------|
| **Large Migrations** | Parallel execution across files/modules | JS → TypeScript migration |
| **Bulk Refactoring** | Independent subtasks | Extract 500 components to library |
| **Multi-Service Changes** | Work across repos simultaneously | API version update across 10 services |
| **Test Generation** | Parallel test creation | Write tests for 100 modules |
| **Documentation** | Parallel page generation | Generate docs for entire API |
| **Data Processing** | Chunked parallel processing | Process 10K records in batches |
| **Code Review** | Parallel PR review | Review 20 pending PRs |

**❌ Not Recommended:**

| Scenario | Why Not | Better Approach |
|----------|---------|-----------------|
| Single small task | Overhead exceeds benefit | Single Devin session |
| Highly interdependent work | Workers block each other | Sequential with checkpoints |
| Exploratory/creative work | Needs human judgment | Human + single Devin |
| Tight budget constraints | Multiple VMs = higher ACU cost | Single agent, longer time |

---

## 🏗️ Part 2: Architecture Patterns

### Pattern 1: Fan-Out/Fan-In (Most Common)

**How It Works:**
1. Coordinator analyzes task and identifies independent subtasks
2. Spawns N worker Devins, assigns one subtask each
3. Workers execute in parallel
4. Coordinator collects results, merges, validates

**Best For:** Bulk operations, migrations, parallel test generation

```
                    COORDINATOR
                        │
         ┌──────────────┼──────────────┐
         │              │              │
         ▼              ▼              ▼
    ┌─────────┐   ┌─────────┐   ┌─────────┐
    │ Worker  │   │ Worker  │   │ Worker  │
    │   A     │   │   B     │   │   C     │
    └────┬────┘   └────┬────┘   └────┬────┘
         │              │              │
         └──────────────┼──────────────┘
                        ▼
                   MERGE & VALIDATE
```

**Example Prompt:**
```markdown
I need to migrate our entire codebase from JavaScript to TypeScript.

**Scope:**
- 150 files in src/ directory
- Each file can be migrated independently
- Target: strict TypeScript, no `any` types

**Your Role as Coordinator:**
1. Analyze all files and group by complexity (simple, medium, complex)
2. Spawn 5 worker Devins
3. Assign 30 files to each worker
4. Provide each worker with:
   - Migration playbook (attached)
   - Type definitions location
   - Testing instructions
5. Track progress, help workers that get stuck
6. Merge all migrated files
7. Run full type check and fix any remaining errors

**Success Criteria:**
- All 150 files converted to .ts
- TypeScript compiler passes with 0 errors
- All existing tests pass
- No `any` types introduced
```

---

### Pattern 2: Pipeline/Sequential

**How It Works:**
1. Coordinator passes work through specialized workers in sequence
2. Each worker adds value/refinement
3. Final worker delivers polished result

**Best For:** Content workflows, multi-stage processing, research pipelines

```
COORDINATOR → Research → Analysis → Writing → Review → Publish
                  ↓          ↓          ↓         ↓        ↓
              Worker 1   Worker 2   Worker 3  Worker 4  Worker 5
```

**Example Prompt:**
```markdown
Create a comprehensive competitive analysis report.

**Pipeline:**
1. **Research Worker**: Gather info on 10 competitors (pricing, features, positioning)
2. **Analysis Worker**: Identify patterns, gaps, opportunities
3. **Writing Worker**: Draft report with executive summary
4. **Review Worker**: Fact-check, add data visualizations
5. **Publish Worker**: Format as PDF, upload to shared drive

**Your Role:**
- Pass context between workers
- Ensure each worker completes before next starts
- Quality check at each stage
- Handle any worker failures
```

---

### Pattern 3: Hierarchical/Manager-Worker

**How It Works:**
1. Manager Devin delegates to multiple workers
2. Workers report back with results
3. Manager evaluates, accepts, or requests revisions
4. Iterates until quality threshold met

**Best For:** Complex projects requiring judgment, variable-quality outputs

```
                    MANAGER
                   /   |   \
                  /    |    \
                 ▼     ▼     ▼
            Worker A  Worker B  Worker C
                 │     │     │
                 └─────┼─────┘
                       ▼
                 EVALUATE
                /         \
           Accept       Revise
```

**Example Prompt:**
```markdown
Build a complete e-commerce website with these features:
- Product catalog
- Shopping cart
- Checkout flow
- User authentication
- Admin dashboard

**Your Role as Manager:**
1. Break down into 5 major components
2. Assign each to a specialized worker:
   - Frontend Worker (React components)
   - Backend Worker (API endpoints)
   - Database Worker (schema, migrations)
   - Auth Worker (authentication, authorization)
   - Testing Worker (E2E tests)
3. Review each worker's output
4. If quality < 80%, request specific revisions
5. Integrate all components
6. Deploy to staging

**Quality Gates:**
- Code review passes
- All tests pass
- Security scan clean
- Performance benchmarks met
```

---

### Pattern 4: Map-Reduce for Code

**How It Works:**
1. Map: Spawn workers to process code chunks independently
2. Reduce: Merge changes, resolve conflicts, validate

**Best For:** Large-scale refactors, bulk updates, repository-wide changes

```
         COORDINATOR
             │
    ┌────────┼────────┐
    │        │        │
    ▼        ▼        ▼
  Map 1    Map 2    Map 3
  (50 files) (50 files) (50 files)
    │        │        │
    └────────┼────────┘
             ▼
        REDUCE
    (Merge + Resolve)
```

---

## 🛠️ Part 3: Step-by-Step Setup Guide

### Step 1: Enable Advanced Capabilities

**Prerequisites:**
- Devin Pro or Enterprise plan (Managed Devins not available on Free tier)
- Advanced Capabilities enabled in settings
- Sufficient ACU quota (parallel workers multiply cost)

**Setup:**
```
1. Go to app.devin.ai/settings
2. Navigate to "Advanced Capabilities"
3. Enable "Managed Devins" toggle
4. Set max parallel workers (recommended: 5-10 for most tasks)
5. Configure ACU budget per worker
```

---

### Step 2: Design Your Coordinator Prompt

**Template:**

```markdown
# Coordinator Devin: [Task Name]

## Objective
[Clear one-sentence goal]

## Scope
- Total work items: [number]
- Estimated subtasks: [number]
- Expected duration: [time]

## Worker Configuration
- Number of workers to spawn: [N]
- Worker type: [specialist/generalist]
- Max ACU per worker: [budget]
- Timeout per worker: [duration]

## Task Decomposition Rules
1. [How to break down work]
2. [Dependency handling]
3. [Priority assignment]

## Worker Instructions Template
[Copy this to each worker:]
"""
You are working on [specific subtask].
Your goals:
1. [Goal 1]
2. [Goal 2]

Constraints:
- [Constraint 1]
- [Constraint 2]

Deliverables:
- [Deliverable 1]
- [Deliverable 2]

Report back when complete with:
- Summary of changes
- Files modified
- Tests run
- Issues encountered
"""

## Progress Tracking
- Check interval: [every X minutes]
- Status format: [template]
- Escalation trigger: [when to intervene]

## Quality Control
- Acceptance criteria: [list]
- Review process: [steps]
- Rejection handling: [retry/revise/reassign]

## Merge Strategy
- How to combine results: [approach]
- Conflict resolution: [process]
- Final validation: [tests/checks]

## Error Handling
- Worker timeout: [action]
- Worker failure: [retry count, then what]
- Partial success: [proceed or rollback]

## Success Criteria
[Clear, measurable completion criteria]
```

---

### Step 3: Spawn Workers

**Method 1: Natural Language (Recommended)**

```
"Spawn 5 worker Devins to help with this migration. 
Each worker should handle 30 files. Name them Worker-1 through Worker-5."
```

**Method 2: Explicit Configuration**

```
"Create worker pool with these settings:
- Pool name: migration-workers
- Worker count: 5
- Worker spec: TypeScript migration specialist
- Per-worker budget: 50 ACU
- Timeout: 30 minutes per worker
- Isolation: full (separate VM, no shared state)"
```

**Method 3: Programmatic (API)**

```python
from devin_sdk import DevinClient

client = DevinClient(api_key="your-key")

# Create coordinator session
coordinator = client.create_session(
    model="devin-v3-enterprise",
    mode="coordinator"
)

# Spawn workers
workers = coordinator.spawn_workers(
    count=5,
    spec={
        "role": "typescript-migration-specialist",
        "max_acu": 50,
        "timeout_minutes": 30
    }
)

# Assign tasks
for i, worker in enumerate(workers):
    files = all_files[i*30:(i+1)*30]
    worker.assign_task(
        instruction=migration_prompt,
        context={"files": files, "batch_id": i}
    )

# Monitor progress
coordinator.monitor_workers(workers, check_interval="5m")

# Merge results
final_result = coordinator.merge(worker_results)
```

---

### Step 4: Assign Tasks to Workers

**Best Practices:**

1. **Clear Boundaries**
   ```
   ✅ Good: "Migrate files 1-30 in src/components/"
   ❌ Bad: "Help with the migration"
   ```

2. **Include Context**
   ```
   ✅ Good: "Here's the migration playbook, type definitions, and 3 examples"
   ❌ Bad: "Migrate these files" (no guidance)
   ```

3. **Define Deliverables**
   ```
   ✅ Good: "Return: migrated files, test results, ACU usage, issues log"
   ❌ Bad: "Let me know when done"
   ```

4. **Set Expectations**
   ```
   ✅ Good: "Expected time: 20-30 min. Escalate if stuck >10 min"
   ❌ Bad: No timeline
   ```

---

### Step 5: Monitor and Manage

**Coordinator Dashboard:**

```
┌─────────────────────────────────────────────────────────────┐
│  MANAGED DEVINS - SESSION #12345                            │
├─────────────────────────────────────────────────────────────┤
│  Status: IN PROGRESS (45 min elapsed)                       │
│  Workers: 5 total | 3 complete | 2 running | 0 failed       │
├─────────────────────────────────────────────────────────────┤
│  WORKER STATUS                                              │
│  ─────────────────────────────────────────────────────────  │
│  Worker-1: ✅ COMPLETE (28 min, 42 ACU)                     │
│  Worker-2: ✅ COMPLETE (31 min, 45 ACU)                     │
│  Worker-3: ✅ COMPLETE (26 min, 39 ACU)                     │
│  Worker-4: 🔄 RUNNING (18 min, 28 ACU) - 70% complete       │
│  Worker-5: 🔄 RUNNING (18 min, 30 ACU) - 65% complete       │
├─────────────────────────────────────────────────────────────┤
│  TOTAL ACU: 184 / 250 budget                                │
│  EST. COMPLETION: 12 minutes                                │
└─────────────────────────────────────────────────────────────┘
```

**Intervention Triggers:**

| Situation | Action |
|-----------|--------|
| Worker stuck >10 min | Check in, offer help |
| Worker error | Review error, retry or reassign |
| Worker off-track | Redirect with specific guidance |
| Worker too slow | Consider splitting task |
| Budget exceeded | Pause, reassess scope |

**Helpful Commands:**

```
/status worker-4          # Check specific worker status
/help worker-3 "..."      # Send guidance to worker
/retry worker-2           # Retry failed worker
/reassign worker-1 to X   # Move task to different worker
/pause all                # Pause all workers
/resume all               # Resume paused workers
```

---

### Step 6: Merge and Validate

**Merge Strategies:**

1. **Simple Concatenation** (independent files)
   ```
   Just combine all worker outputs
   ```

2. **Conflict Resolution** (overlapping changes)
   ```
   - Auto-merge non-conflicting changes
   - Flag conflicts for coordinator review
   - Coordinator resolves or escalates to human
   ```

3. **Integration Testing** (interdependent work)
   ```
   - Merge all changes
   - Run integration test suite
   - Fix any breaking issues
   ```

**Validation Checklist:**

```
□ All workers completed successfully
□ All deliverables received
□ Quality meets acceptance criteria
□ Tests pass (unit + integration)
□ No regressions introduced
□ Documentation updated
□ ACU within budget
□ Ready for human review
```

---

## 📊 Part 4: Real-World Examples

### Example 1: Monolith to Microservices Migration

**Context:** Nubank's ETL migration (6M lines of code, 100K data classes)

**Coordinator Setup:**

```markdown
# Coordinator: ETL Monolith → Sub-modules Migration

## Objective
Migrate 100,000 data class implementations from monolithic ETL to independent sub-modules.

## Worker Pool
- 50 workers running in parallel
- Each worker handles 2,000 data classes
- Worker type: Migration specialist (fine-tuned on migration examples)
- Budget: 50 ACU per worker (2,500 total)
- Timeout: 30 minutes per worker

## Task Decomposition
1. Group data classes by business domain (Collections, Risk, Data, etc.)
2. Within each domain, group by dependency order
3. Assign batches to workers

## Worker Instructions
"You are migrating data classes from monolith to sub-module.

For each data class:
1. Identify source file and dependencies
2. Create new file in target sub-module
3. Update all imports (old → new paths)
4. Verify no circular dependencies
5. Run unit tests for migrated class
6. Log any errors or edge cases

Use the migration playbook for patterns. When in doubt, check similar migrations in examples/."

## Progress Tracking
- Check every 5 minutes
- Workers report: completed count, errors, ACU used
- Escalate if error rate >5%

## Quality Gates
- 100% of classes migrated
- Zero circular dependencies
- All unit tests pass
- Import paths verified

## Merge Strategy
- Auto-merge all successful migrations
- Coordinator reviews error log
- Retry failed migrations with manual guidance
```

**Results:**
- **Before:** 18 months, 1,000 engineers
- **After:** Weeks, 50 parallel Devins
- **Efficiency:** 8-12x improvement
- **Cost:** 20x savings

---

### Example 2: Enterprise-Wide TypeScript Migration

**Context:** 150K lines of JavaScript across 20 repositories

**Coordinator Setup:**

```markdown
# Coordinator: JavaScript → TypeScript Migration

## Objective
Migrate entire codebase to strict TypeScript with zero `any` types.

## Worker Pool
- 10 workers (2 per repository)
- Worker A: Core logic migration
- Worker B: UI components migration
- Budget: 100 ACU per worker

## Repository Assignment
Repo-1: Worker-1A, Worker-1B
Repo-2: Worker-2A, Worker-2B
...

## Worker Instructions (Core Logic)
"Migrate JavaScript files to TypeScript:
1. Add type annotations to all functions
2. Create interfaces for objects
3. No `any` types allowed
4. Use strict mode
5. Fix all type errors before completing

Files: src/**/*.js (excluding tests)"

## Worker Instructions (UI Components)
"Migrate React components to TypeScript:
1. Convert .jsx to .tsx
2. Type all props with interfaces
3. Type all state and hooks
4. Fix all TypeScript errors
5. Verify components still render

Files: src/components/**/*.jsx"

## Coordination Rules
- Core logic workers finish first (types needed by UI)
- UI workers wait for core types
- Shared types go in @company/types package

## Validation
- `tsc --noEmit` passes with 0 errors
- All existing tests pass
- No `any` in codebase
- Build succeeds
```

---

### Example 3: Bulk Test Generation

**Context:** Add unit tests to 200 modules with 80%+ coverage

**Coordinator Setup:**

```markdown
# Coordinator: Test Generation Sprint

## Objective
Generate comprehensive unit tests for 200 modules across 5 services.

## Worker Pool
- 20 workers (4 per service)
- Each worker handles 10 modules
- Worker type: Test specialist
- Budget: 30 ACU per worker

## Worker Instructions
"Generate unit tests for assigned modules:

For each module:
1. Analyze all public functions
2. Write tests for:
   - Happy path (normal inputs)
   - Edge cases (null, empty, boundaries)
   - Error cases (invalid inputs, failures)
3. Mock external dependencies
4. Target 80%+ coverage
5. All tests must pass

Deliverables:
- Test files (test_*.py or *.test.js)
- Coverage report
- List of any modules that need manual review"

## Quality Control
- Coordinator samples 10% of tests
- Coverage verified automatically
- Flaky tests flagged for review

## Merge
- All test files committed to respective services
- Coverage reports aggregated
- Summary dashboard created
```

---

### Example 4: Multi-Repo API Update

**Context:** Update 15 microservices to new API version

**Coordinator Setup:**

```markdown
# Coordinator: API v2 → v3 Migration

## Objective
Update all 15 microservices to use API v3 endpoints.

## Worker Pool
- 15 workers (1 per service)
- Each worker owns one service
- Budget: 75 ACU per worker

## Worker Instructions
"Migrate [Service Name] to API v3:

1. Read API v3 changelog (attached)
2. Identify all API calls in service
3. Update endpoints: v2/* → v3/*
4. Update request/response types
5. Handle breaking changes:
   - Auth header format changed
   - Pagination response structure changed
   - Error codes remapped
6. Update integration tests
7. Deploy to staging, verify

Breaking Changes Reference:
- Auth: `Authorization: Bearer X` → `X-API-Key: X`
- Pagination: `{data, total}` → `{items, meta: {total}}`
- Errors: 400 → 422 for validation errors"

## Coordination
- Shared authentication library updated first
- All services must complete before production rollout
- Coordinator tracks completion % per service

## Validation
- All integration tests pass
- API response times within 10% of baseline
- No 5xx errors in staging (24h monitoring)
```

---

## 💡 Part 5: Best Practices

### Prompt Engineering for Coordinators

**1. Be Explicit About Parallelism**

```
✅ Good: "Spawn 10 workers to handle this in parallel"
❌ Bad: "Get this done somehow"
```

**2. Define Clear Handoff Points**

```
✅ Good: "Worker A completes schema changes, then signals Worker B to start migrations"
❌ Bad: "Everyone work on the database stuff"
```

**3. Set Budget Expectations**

```
✅ Good: "Each worker has 50 ACU budget. Alert me at 80% usage"
❌ Bad: "Don't spend too much"
```

**4. Specify Quality Thresholds**

```
✅ Good: "Accept worker output if tests pass and coverage >80%"
❌ Bad: "Make sure it's good"
```

---

### Worker Management

**1. Right-Size Your Worker Pool**

| Total Work | Recommended Workers | Rationale |
|------------|---------------------|-----------|
| <10 subtasks | 1-2 | Overhead not worth it |
| 10-50 subtasks | 3-5 | Good parallelism |
| 50-200 subtasks | 5-15 | Maximum efficiency |
| 200+ subtasks | 15-50 | Enterprise scale |

**2. Monitor Proactively**

```
✅ Check every 5-10 minutes
✅ Set up alerts for failures
✅ Review worker logs for patterns
❌ Set and forget
❌ Wait for all workers to finish before checking
```

**3. Handle Failures Gracefully**

```
On worker failure:
1. Review error message
2. Determine if retryable
3. If yes: retry with additional context
4. If no: reassign to different worker or handle manually
5. Log failure for pattern analysis
```

---

### Cost Optimization

**ACU Budget Planning:**

```
Total Budget = (Workers × Per-Worker Budget) + Coordinator Overhead

Example:
- 10 workers × 50 ACU = 500 ACU
- Coordinator overhead = 100 ACU
- Total budget = 600 ACU

Add 20% buffer for retries and edge cases:
- Final budget = 720 ACU
```

**Cost-Saving Tips:**

1. **Right-size workers:** Don't spawn 10 workers for 5 tasks
2. **Set timeouts:** Prevent runaway workers
3. **Use specialists:** Fine-tuned workers complete tasks faster
4. **Batch similar work:** Reduce context-switching overhead
5. **Monitor ACU burn:** Alert at 50%, 75%, 90% of budget

---

### Error Prevention

**Common Issues & Solutions:**

| Issue | Cause | Solution |
|-------|-------|----------|
| Workers duplicate work | Unclear task boundaries | Assign explicit file ranges/IDs |
| Workers block each other | Hidden dependencies | Map dependencies before spawning |
| Inconsistent output quality | Varying worker capabilities | Provide detailed examples |
| Budget overruns | No per-worker limits | Set hard ACU caps |
| Merge conflicts | Overlapping changes | Use exclusive file assignments |
| Workers get stuck | Ambiguous instructions | Add escalation triggers |

---

## 📈 Part 6: Metrics and Optimization

### Key Metrics to Track

| Metric | Formula | Target | Why It Matters |
|--------|---------|--------|----------------|
| **Parallelization Efficiency** | (Sequential Time) / (Parallel Time) | 5-10x | Measures speedup from parallelism |
| **Worker Success Rate** | (Successful Workers) / (Total Workers) | 90%+ | Indicates task clarity |
| **ACU per Subtask** | (Total ACU) / (Subtasks Completed) | decreasing | Shows learning curve |
| **Coordinator Overhead** | (Coordinator ACU) / (Total ACU) | <20% | Measures orchestration efficiency |
| **Retry Rate** | (Retried Workers) / (Total Workers) | <10% | Indicates instruction quality |
| **Merge Conflict Rate** | (Conflicts) / (Total Changes) | <5% | Shows task independence |

---

### Continuous Improvement Loop

```
1. Run Managed Devins session
       ↓
2. Collect metrics (time, ACU, success rate)
       ↓
3. Identify bottlenecks (which workers struggled?)
       ↓
4. Analyze root causes (instructions? dependencies? skills?)
       ↓
5. Update playbook/templates
       ↓
6. Run improved session
       ↓
7. Compare metrics, iterate
```

---

### Learning from Nubank: Key Insights

**What Made Their Success:**

1. **Fine-Tuning Paid Off**
   - Collected 100+ migration examples
   - Fine-tuned Devin on these examples
   - Result: 2x completion rate, 4x speed

2. **Progressive Improvement**
   - First week: Many errors, slow
   - Second week: Fewer errors, faster
   - Third week: Smooth execution
   - *Lesson: Let workers learn from patterns*

3. **Self-Improving Tools**
   - Devin built scripts to automate repetitive parts
   - Scripts reused across all workers
   - *Lesson: Let workers optimize their own workflows*

4. **Human-in-the-Loop**
   - Engineers reviewed, didn't implement
   - Quick feedback on edge cases
   - *Lesson: Keep humans for judgment, not grunt work*

---

## 🎓 Part 7: Learning Path

### Week 1-2: Foundations
- [ ] Complete single-Devin tasks (build comfort with Devin)
- [ ] Read this guide completely
- [ ] Set up Advanced Capabilities
- [ ] Run first Managed Devins session (small task, 2-3 workers)

### Week 3-4: First Projects
- [ ] Choose a bulk operation (test generation, documentation)
- [ ] Design coordinator prompt using template
- [ ] Run with 5 workers
- [ ] Analyze results, document learnings

### Week 5-8: Intermediate
- [ ] Tackle a migration project
- [ ] Use 10+ workers
- [ ] Implement progress tracking
- [ ] Handle worker failures gracefully
- [ ] Optimize ACU usage

### Week 9+: Advanced
- [ ] Run enterprise-scale project (50+ workers)
- [ ] Create custom worker playbooks
- [ ] Fine-tune workers for your use case
- [ ] Build metrics dashboard
- [ ] Train team on Managed Devins

---

## 📖 Part 8: Resources

### Official Documentation
- [Managed Devins Announcement](https://cognition.ai/blog/devin-can-now-manage-devins)
- [Advanced Capabilities Docs](https://docs.devin.ai/product-guides/advanced-capabilities)
- [API Reference](https://docs.devin.ai/api-reference/overview)

### Tools & Templates
- **Coordinator Prompt Template:** See Part 3, Step 2
- **Worker Instructions Template:** See Part 3, Step 4
- **Metrics Dashboard:** Build using Devin Analytics API

### Community
- [Cognition Slack](https://app.devin.ai/settings/support)
- [Managed Devins Showcase](https://devin.ai/community/showcase)
- [Best Practices Forum](https://community.cognition.ai/)

---

## 🎯 Quick Reference

### Before Starting

```
□ Task is large enough to justify parallelism (10+ subtasks)
□ Subtasks are independent or have clear dependencies
□ Budget allows for multiple workers (N × per-worker ACU)
□ You have time to monitor and manage workers
□ Acceptance criteria are clear and measurable
```

### Coordinator Checklist

```
□ Clear objective defined
□ Worker pool size determined
□ Per-worker budget set
□ Task decomposition complete
□ Worker instructions written
□ Progress tracking configured
□ Quality gates defined
□ Error handling planned
□ Merge strategy documented
```

### During Execution

```
□ Check progress every 5-10 minutes
□ Review worker logs for patterns
□ Help stuck workers promptly
□ Track ACU burn rate
□ Document issues for future improvement
```

### After Completion

```
□ All deliverables received
□ Quality validated
□ Metrics collected
□ Learnings documented
□ Playbook updated
□ Team briefed on results
```

---

**Last Updated:** April 13, 2026  
**Author:** weisenaibot 🐺  
**License:** Internal use only  
**Based on:** Official Cognition AI announcements + Nubank case study + industry research
