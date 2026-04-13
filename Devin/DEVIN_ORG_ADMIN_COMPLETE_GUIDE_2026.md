# Devin Organization Management: Complete Admin Guide 2026

**Created:** April 13, 2026  
**Version:** 1.0  
**Sources:** Official Devin Docs + Mercari Enterprise Case Study + Cognition AI Announcements + Industry Best Practices

---

## 🎯 Executive Summary

**Devin Enterprise** provides centralized management of multiple Devin organizations through an Enterprise management layer. This guide covers everything org admins need to know about managing Devin at scale.

**Key Enterprise Features (2026):**
- ✅ **Multi-Org Management** - Centralized control of 10+ organizations
- ✅ **Enterprise API v3** - Full automation of members, roles, secrets, knowledge
- ✅ **SSO Integration** - Okta, GitHub Enterprise, Google Workspace
- ✅ **Audit Logging** - Complete activity tracking for compliance
- ✅ **ACU Governance** - Budget controls, visibility, hard caps
- ✅ **Secret Management** - Enterprise-scoped secrets, automated rotation
- ✅ **MCP Registry Enforcement** - Allowlist control across organizations
- ✅ **Build Pinning** - Version control and rollback capabilities

**Real-World Scale (Mercari Case Study):**
- **10+ Organizations** managed in parallel
- **Custom Terraform Provider** for IaC management
- **Automated Secret Rotation** via GitHub Actions
- **Security Monitoring Integration** for audit compliance
- **API Key Lifecycle Management** with auto-expiration

---

## 📋 Part 1: Enterprise Architecture

### Enterprise vs Organization Structure

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENTERPRISE ACCOUNT                            │
│  (Central Management Layer)                                     │
│                                                                  │
│  Enterprise Admins                                               │
│  • Manage all organizations                                      │
│  • Set enterprise-wide policies                                  │
│  • View consolidated usage                                       │
│  • Enforce security controls                                     │
│                                                                  │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │  ENTERPRISE API v3                                         │  │
│  │  • Members API    • Secrets API                           │  │
│  │  • Roles API      • Knowledge API                         │  │
│  │  • Audit Logs     • Consumption API                       │  │
│  └───────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
         │                    │                    │
         ▼                    ▼                    ▼
┌───────────────┐   ┌───────────────┐   ┌───────────────┐
│ ORG 1         │   │ ORG 2         │   │ ORG 3         │
│ (Team A)      │   │ (Team B)      │   │ (Team C)      │
│               │   │               │   │               │
│ • Members     │   │ • Members     │   │ • Members     │
│ • Repos       │   │ • Repos       │   │ • Repos       │
│ • Secrets     │   │ • Secrets     │   │ • Secrets     │
│ • ACU: 500/mo │   │ • ACU: 300/mo │   │ • ACU: 400/mo │
│ • Isolated    │   │ • Isolated    │   │ • Isolated    │
└───────────────┘   └───────────────┘   └───────────────┘
```

### Plan Comparison

| Feature | Core | Team | Enterprise |
|---------|------|------|------------|
| **Pricing** | $2.25/ACU (pay-as-you-go) | $500/mo (250 ACU included) | Custom |
| **Organizations** | 1 | 1 | Multiple (10+) |
| **SSO** | GitHub/Google | GitHub/Google | SAML, Okta, Custom |
| **ACU Management** | Basic | Basic | Enterprise controls |
| **Audit Logs** | No | No | Yes (v3 API) |
| **Secret Management** | Per-org only | Per-org only | Enterprise-scoped |
| **MCP Enforcement** | No | No | Registry allowlist |
| **Build Pinning** | No | No | Yes |
| **VPC Deployment** | No | No | Yes |
| **API Access** | Limited | Limited | Full v3 API |

---

## 🛠️ Part 2: Organization Setup

### Step 1: Create Enterprise Account

**Prerequisites:**
- Contact Cognition AI sales for Enterprise plan
- Complete security review
- Sign Enterprise agreement

**Initial Setup:**
```
1. Navigate to portal.cognition.ai (Enterprise portal)
2. Complete SSO configuration:
   - SAML 2.0 provider (Okta, Azure AD, etc.)
   - GitHub Enterprise Server (optional)
   - Google Workspace (optional)
3. Create first organization
4. Assign Enterprise admin roles
5. Configure billing and ACU pool
```

### Step 2: Create Organizations

**Organization Structure Best Practices:**

```
Recommended Structure:
├── org-dev-platform      (Platform team)
├── org-dev-frontend      (Frontend team)
├── org-dev-backend       (Backend team)
├── org-dev-mobile        (Mobile team)
├── org-data-science      (Data/ML team)
├── org-security          (Security team - restricted)
├── org-wiki              (Shared knowledge base)
└── org-sandbox           (Testing/experimentation)
```

**Via Web UI:**
```
1. Enterprise Admin Console → Organizations
2. Click "Create Organization"
3. Enter organization name (lowercase, hyphens)
4. Set initial ACU limits:
   - max_cycle_acu_limit: Monthly cap
   - max_session_acu_limit: Per-session cap
5. Configure repository access
6. Add initial members
```

**Via API (Automated):**
```bash
curl -X POST https://api.devin.ai/v3/enterprises/{enterprise_id}/organizations \
  -H "Authorization: Bearer $ENTERPRISE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "mercari-example-team",
    "max_cycle_acu_limit": 500,
    "max_session_acu_limit": 250
  }'
```

### Step 3: Configure ACU Limits

**ACU (Agent Compute Unit) Governance:**

| Limit Type | Purpose | Recommended Values |
|------------|---------|-------------------|
| **max_cycle_acu_limit** | Monthly org budget | 300-1000 per team |
| **max_session_acu_limit** | Per-session cap | 50-250 per session |
| **Enterprise pool** | Total monthly ACUs | Based on team size |

**Example Configuration:**
```terraform
# Terraform example (Mercari's approach)
resource "devin_organization" "platform_team" {
  name                      = "dev-platform"
  max_cycle_acu_limit       = 500
  max_session_acu_limit     = 250
  enterprise_id             = var.enterprise_id
}

resource "devin_organization" "frontend_team" {
  name                      = "dev-frontend"
  max_cycle_acu_limit       = 300
  max_session_acu_limit     = 150
  enterprise_id             = var.enterprise_id
}
```

**ACU Budget Planning:**

```
Formula:
Total Enterprise ACUs = Σ(Org ACU Limits) + 20% buffer

Example (10 organizations):
- 4 dev teams × 500 ACU = 2,000 ACU
- 2 data teams × 400 ACU = 800 ACU
- 1 security team × 300 ACU = 300 ACU
- 1 wiki org × 200 ACU = 200 ACU
- 2 sandbox orgs × 100 ACU = 200 ACU
- Subtotal = 3,500 ACU
- Buffer (20%) = 700 ACU
- Total = 4,200 ACU/month

Cost Estimate (Enterprise pricing ~$2/ACU):
4,200 ACU × $2 = $8,400/month
```

---

## 👥 Part 3: Member & Permission Management

### Role Hierarchy

```
Enterprise Level:
├── Enterprise Owner     (Full access to all orgs)
├── Enterprise Admin     (Management access)
└── Enterprise Member    (Read-only enterprise data)

Organization Level:
├── Org Owner           (Full org access)
├── Org Admin           (Member + repo management)
├── Org Member          (Standard Devin access)
└── Org Viewer          (Read-only sessions)
```

### Adding Members (Manual)

**Via Web UI:**
```
1. Organization Settings → Members
2. Click "Add Member"
3. Enter email address
4. Select role (Member, Admin, Owner)
5. Send invitation
```

### Adding Members (Automated - Recommended)

**Via Terraform (Mercari's Approach):**
```terraform
# Member definition (referenced by email)
data "devin_member" "platform_team" {
  for_each = toset([
    "user-1@example.com",
    "user-2@example.com",
    "user-3@example.com",
  ])
  email = each.value
}

# Assignment to Organization
resource "devin_organization_member" "platform_team" {
  for_each = data.devin_member.platform_team

  user_id     = each.value.user_id
  org_id      = devin_organization.platform_team.org_id
  org_role_id = "org_member"  # or "org_admin", "org_owner"
}
```

**Via API:**
```bash
# Add member to organization
curl -X POST https://api.devin.ai/v3/organizations/{org_id}/members \
  -H "Authorization: Bearer $ENTERPRISE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": "user-123",
    "role_id": "org_member"
  }'
```

### Permission Best Practices

**Principle of Least Privilege:**
```
✅ Do:
- Start users as Org Member
- Promote to Admin only when needed
- Use time-limited admin access
- Review permissions quarterly

❌ Don't:
- Make everyone an Org Owner
- Share admin accounts
- Skip permission reviews
```

**Access Review Checklist:**
```
□ Review member list monthly
□ Remove departed employees within 24h
□ Audit admin access quarterly
□ Verify org isolation is maintained
□ Check for orphaned API keys
```

---

## 🔐 Part 4: Security & Access Control

### SSO Configuration

**Supported Providers:**
- SAML 2.0 (Okta, Azure AD, OneLogin, etc.)
- GitHub Enterprise Server
- Google Workspace
- Custom OIDC

**Okta SSO Setup:**
```
1. Enterprise Settings → Identity Provider
2. Select "SAML 2.0"
3. Download SP metadata from Devin
4. Configure in Okta:
   - Single Sign On URL: https://app.devin.ai/auth/saml
   - Audience URI (SP Entity ID): https://app.devin.ai
   - Name ID Format: emailAddress
5. Upload IdP metadata to Devin
6. Test SSO connection
7. Enable for all organizations
```

### API Key Management

**API Key Types:**
| Type | Scope | Use Case | Management |
|------|-------|----------|------------|
| **User API Keys** | Per-user | Personal automation | Auto-expire (admin policy) |
| **Org API Keys** | Per-org | Service integration | Manual rotation |
| **Enterprise API Keys** | Enterprise-wide | Admin automation | Strict control |

**API Key Lifecycle Policy (Mercari's Approach):**
```
1. All API keys expire after 30 days
2. Automated invalidation via GitHub Actions
3. Service keys stored in Google Secret Manager
4. Keys recreated and rotated weekly
5. Audit log tracks all key usage

Automation Flow:
┌─────────────┐    ┌──────────────┐    ┌─────────────┐
│ GitHub      │    │ Google       │    │ Devin       │
│ Actions     │───▶│ Secret Mgr   │───▶│ API         │
│ (Scheduled) │    │              │    │             │
└─────────────┘    └──────────────┘    └─────────────┘
      │                    │                    │
      ▼                    ▼                    ▼
  Fetch all keys      Store new         Invalidate
  > 30 days old       keys              old keys
```

**API Key Invalidation Script:**
```bash
#!/bin/bash
# Invalidate API keys older than 30 days

THIRTY_DAYS_AGO=$(date -d "30 days ago" -Iseconds)
API_KEYS=$(curl -s https://api.devin.ai/v2/api-keys \
  -H "Authorization: Bearer $ENTERPRISE_API_KEY")

echo "$API_KEYS" | jq -r '.[] | select(.created_at < "'$THIRTY_DAYS_AGO'") | .id' | \
while read key_id; do
  echo "Invalidating key: $key_id"
  curl -X DELETE "https://api.devin.ai/v2/api-keys/$key_id" \
    -H "Authorization: Bearer $ENTERPRISE_API_KEY"
done
```

### Secret Management

**Enterprise-Scoped Secrets (April 2026 Feature):**
```
Benefits:
- Define once, share across all organizations
- Automatic propagation to new orgs
- Centralized rotation
- Audit trail for all access

Use Cases:
- GitHub tokens (shared across orgs)
- Cloud provider credentials
- Third-party API keys
- Database connection strings
```

**Secret Configuration:**
```bash
# Create enterprise-scoped secret
curl -X POST https://api.devin.ai/v3/enterprise/{enterprise_id}/secrets \
  -H "Authorization: Bearer $ENTERPRISE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "GITHUB_TOKEN",
    "value": "ghp_xxxxx",
    "scope": "enterprise",
    "organizations": ["*"]  # All orgs, or specify list
  }'
```

**Bulk Secret Rotation (Automated):**
```yaml
# GitHub Actions workflow
name: Rotate Devin Secrets

on:
  schedule:
    - cron: '0 2 * * 1'  # Weekly, Monday 2 AM
  workflow_dispatch:  # Manual trigger for emergencies

jobs:
  rotate-secrets:
    runs-on: ubuntu-latest
    steps:
      - name: Fetch new credentials from Secret Manager
        uses: google-github-actions/auth@v2
        with:
          workload_identity_provider: ${{ secrets.WIF_PROVIDER }}
          service_account: ${{ secrets.SA_EMAIL }}
      
      - name: Get new GitHub token
        id: github-token
        run: |
          NEW_TOKEN=$(gcloud secrets versions access latest \
            --secret="github-token" \
            --project="my-project")
          echo "token=$NEW_TOKEN" >> $GITHUB_OUTPUT
      
      - name: Rotate across all organizations
        run: |
          ORGS=$(curl -s https://api.devin.ai/v3/organizations \
            -H "Authorization: Bearer $ENTERPRISE_API_KEY")
          
          echo "$ORGS" | jq -r '.[].id' | while read org_id; do
            curl -X PUT "https://api.devin.ai/v3/organizations/$org_id/secrets/GITHUB_TOKEN" \
              -H "Authorization: Bearer $ENTERPRISE_API_KEY" \
              -d "{\"value\": \"${{ steps.github-token.outputs.token }}\"}"
            echo "Rotated secret for org: $org_id"
          done
```

---

## 📊 Part 5: Usage Analytics & Cost Control

### Consumption Dashboard

**Enterprise Consumption View:**
```
Metrics Available:
├── Total ACU Consumption (current vs previous cycle)
├── ACU by Organization
├── ACU by User
├── ACU by Product (Sessions, Review, Indexing, Wiki)
├── Session Count & Duration
├── Top Repositories
└── Cost Projection (current run rate)
```

**Usage Table (New April 2026):**
| User | Sessions | Review ACU | Session ACU | Total ACU | Trend |
|------|----------|------------|-------------|-----------|-------|
| user1@co.com | 45 | 120 | 380 | 500 | ↑ 12% |
| user2@co.com | 32 | 80 | 220 | 300 | → 0% |
| user3@co.com | 28 | 60 | 190 | 250 | ↓ 8% |

### ACU Hard Caps (April 2026 Feature)

**Session-Level Hard Caps:**
```
Purpose: Prevent runaway sessions from consuming excessive ACUs

Configuration:
- Enterprise Admin → Settings → ACU Controls
- Set max_session_acu_limit (e.g., 250 ACU)
- Users see warning at 80% usage
- Session auto-stops at 100%

Benefits:
- Prevents surprise overages
- Forces users to be intentional
- Easier budget forecasting
```

**Alert Configuration:**
```yaml
# ACU Alert Thresholds
alerts:
  - threshold: 50%    # Notification
  - threshold: 80%    # Warning (user sees modal)
  - threshold: 100%   # Hard stop (session ends)
```

### Cost Optimization Strategies

**1. Right-Size Organization Limits**
```
Before: All orgs get 500 ACU/month
After: Based on team size and usage patterns

Small teams (1-3 devs):    200 ACU/month
Medium teams (4-8 devs):   400 ACU/month
Large teams (9+ devs):     800 ACU/month
```

**2. Use Managed Devins Efficiently**
```
Parallel workers multiply ACU consumption:
- 1 worker = 1x ACU
- 10 workers = 10x ACU (but 5-10x faster)

Optimization:
- Use for large tasks only (10+ subtasks)
- Set per-worker ACU budgets
- Monitor parallel efficiency
```

**3. Archive Old Sessions**
```
Sessions consume storage and may incur costs:
- Archive sessions >90 days old
- Export important sessions before archiving
- Keep active sessions <30 days
```

**4. Optimize Wiki Generation**
```
DeepWiki costs vary by effort level:
- Quick: ~10 ACU (surface-level docs)
- Standard: ~50 ACU (comprehensive)
- Deep: ~200 ACU (exhaustive)

Optimization:
- Use "Quick" for routine updates
- Reserve "Deep" for major releases
- Review cost breakdown before regenerating
```

---

## 🔌 Part 6: MCP Server Management

### MCP Registry Enforcement (April 2026 Feature)

**Enterprise MCP Allowlist:**
```
Purpose: Control which MCP servers can be used across all organizations

Configuration:
1. Enterprise Admin → MCP Registry
2. Add approved MCP servers:
   - GitHub MCP Server
   - Linear MCP Server
   - Amplitude MCP Server
   - Custom internal MCPs
3. Enforce allowlist across all orgs
4. Block unapproved MCPs
```

**Approved MCP Servers:**
```yaml
# Example Enterprise MCP Allowlist
allowed_mcp_servers:
  - name: github
    url: https://github-mcp.devin.ai
    oauth_required: true
    
  - name: linear
    url: https://linear-mcp.devin.ai
    oauth_required: true
    
  - name: amplitude
    url: https://amplitude-mcp.devin.ai
    oauth_required: true
    
  - name: internal-wiki
    url: https://wiki-mcp.internal.company.com
    oauth_required: false
    auth: service_account
```

### Personal MCP Servers (April 2026 Feature)

**User-Managed MCPs:**
```
Purpose: Allow users to connect personal MCP servers without org-wide approval

Use Cases:
- Personal productivity tools
- Experimental MCPs
- Individual developer workflows

Configuration:
- User Settings → MCP Servers → Add Personal
- Personal MCPs only visible to user
- No org secret access
- Audit logged for compliance
```

### MCP Audit Logs (April 2026 Feature)

**Tracked Events:**
```
- MCP server installation
- MCP server updates
- Secret link/unlink events
- MCP usage per session
- OAuth authorization events

Access:
Enterprise Admin → Audit Logs → Filter: MCP Events
```

---

## 📝 Part 7: Knowledge & Skills Management

### Enterprise Knowledge Base

**Knowledge Distribution (Mercari's Approach):**
```
Challenge: Organizations are isolated, but teams need to share best practices

Solution: Manage Knowledge via Terraform for cross-org distribution

resource "devin_knowledge" "best_practices" {
  name        = "devin-best-practices"
  content     = file("${path.module}/knowledge/best-practices.md")
  target_orgs = [
    devin_organization.platform_team.org_id,
    devin_organization.frontend_team.org_id,
    devin_organization.backend_team.org_id,
  ]
}
```

**Knowledge Types:**
| Type | Scope | Content |
|------|-------|---------|
| **Org Knowledge** | Single org | Team-specific practices |
| **Enterprise Knowledge** | Multiple orgs | Shared best practices |
| **Personal Knowledge** | User only | Individual notes |

### Skills Distribution

**Skill Management:**
```
Skills (Agent Skills/Playbooks) can be:
- Created per organization
- Distributed via Enterprise API
- Versioned and updated centrally

Distribution Flow:
1. Create skill in org-dev-platform
2. Export skill package
3. Import to other orgs via API
4. Track usage across orgs
```

---

## 🔍 Part 8: Audit & Compliance

### Audit Log Configuration

**Audit Log Events:**
```
Session Events:
- Session created
- Session completed
- Session failed
- ACU consumption

Member Events:
- Member added
- Member removed
- Role changed
- API key created/revoked

Security Events:
- Secret accessed
- MCP server connected
- Repository linked
- Permission denied

Admin Events:
- Org created/deleted
- ACU limit changed
- Policy updated
- Build pinned
```

### Log Export & Analysis (Mercari's Setup)

**Architecture:**
```
┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌─────────────┐
│ Devin       │    │ Cloud Run    │    │ Pub/Sub     │    │ BigQuery    │
│ Audit API   │───▶│ Job          │───▶│             │───▶│             │
│ (v3)        │    │ (Scheduled)  │    │             │    │ (Analysis)  │
└─────────────┘    └──────────────┘    └─────────────┘    └─────────────┘
```

**Implementation:**
```python
# Cloud Run Job - Audit Log Collector
import requests
from google.cloud import pubsub_v1

DEVIN_API = "https://api.devin.ai/v3/audit-logs"
PUBSUB_TOPIC = "projects/my-project/topics/devin-audit-logs"

def fetch_and_forward_logs():
    # Fetch logs with pagination
    logs = []
    cursor = None
    while True:
        params = {"cursor": cursor} if cursor else {}
        response = requests.get(
            DEVIN_API,
            headers={"Authorization": f"Bearer {os.environ['DEVIN_API_KEY']}"},
            params=params
        )
        data = response.json()
        logs.extend(data["logs"])
        
        if not data.get("next_cursor"):
            break
        cursor = data["next_cursor"]
    
    # Forward to Pub/Sub
    publisher = pubsub_v1.PublisherClient()
    for log in logs:
        publisher.publish(
            topic=PUBSUB_TOPIC,
            data=json.dumps(log).encode()
        )
    
    return f"Forwarded {len(logs)} logs"
```

### Compliance Checklist

```
□ Audit logs enabled and exporting
□ Logs retained for required period (90 days min)
□ Access reviews conducted quarterly
□ API key rotation automated
□ SSO enforced for all users
□ MCP allowlist configured
□ ACU limits set for all orgs
□ Incident response plan documented
□ Security training completed
```

---

## 🚀 Part 9: Automation & IaC

### Custom Terraform Provider (Mercari's Approach)

**Why Terraform:**
- Standard IaC tool at most companies
- PR review process for changes
- State visibility
- Rollback capability

**Provider Resources:**
```terraform
# Organization management
resource "devin_organization" "example" {
  name                      = "example-team"
  max_cycle_acu_limit       = 500
  max_session_acu_limit     = 250
  enterprise_id             = var.enterprise_id
}

# Member management
data "devin_member" "users" {
  for_each = toset(var.user_emails)
  email    = each.value
}

resource "devin_organization_member" "assignments" {
  for_each = data.devin_member.users
  user_id  = each.value.user_id
  org_id   = devin_organization.example.org_id
  org_role_id = "org_member"
}

# Knowledge distribution
resource "devin_knowledge" "shared" {
  name        = "best-practices"
  content     = file("./knowledge/best-practices.md")
  target_orgs = var.target_org_ids
}
```

**Workflow:**
```
1. Engineer modifies Terraform
2. Opens PR with changes
3. Team reviews (who's being added/removed)
4. Merge applies changes
5. State updated, audit logged
```

### GitHub Actions Automation

**Management Operations Automated:**
```yaml
# Scheduled Operations
- Secret rotation (weekly)
- API key invalidation (daily)
- ACU usage report (daily)
- Audit log export (hourly)

# Event-Triggered Operations
- New org setup (on Terraform merge)
- Member onboarding (HR system webhook)
- Emergency key revocation (manual)
```

---

## 📖 Part 10: Real-World Case Studies

### Mercari: Secure Devin Management at Scale

**Challenge:**
- 10+ organizations across multiple teams
- Manual member management was time-consuming
- Secret rotation across orgs was burdensome
- API key lifecycle not managed
- Audit compliance requirements

**Solution:**
1. **Custom Terraform Provider** - IaC for orgs and members
2. **Bulk Secret Rotation** - Automated via GitHub Actions
3. **API Key Management** - Auto-expire after 30 days
4. **Audit Integration** - Forward logs to security platform
5. **Service Account Rotation** - GCP key rotation automation

**Results:**
- ✅ 10+ organizations managed in parallel
- ✅ Zero manual secret rotation
- ✅ Full audit compliance
- ✅ No long-lived credentials
- ✅ Clear visibility into usage

**Key Quote:**
> "Through these tools, we established mechanisms for member and permission management, secret rotation, API key lifecycle management, and auditing. We hope that this serves as a blueprint for securing deploying and operating Devin across an enterprise."
> — Mercari AI Security Team

---

### Nubank: Enterprise Migration at Scale

**Challenge:**
- 6 million lines of code ETL monolith
- 100,000 data class migrations needed
- 1,000 engineers would take 18 months manually

**Solution:**
- Fine-tuned Devin on migration examples
- Parallel Managed Devins (50 workers)
- Human-in-the-loop review process

**Results:**
- **8-12x** efficiency improvement
- **20x** cost savings
- Completed in **weeks** vs. 18 months

---

## 🎓 Part 11: Admin Learning Path

### Week 1-2: Foundations
- [ ] Complete Enterprise onboarding
- [ ] Configure SSO integration
- [ ] Create first 2-3 organizations
- [ ] Add initial members
- [ ] Set ACU limits

### Week 3-4: Security Basics
- [ ] Configure API key policies
- [ ] Set up secret management
- [ ] Enable audit logging
- [ ] Review MCP allowlist
- [ ] Document incident response

### Week 5-8: Automation
- [ ] Build Terraform provider (or use existing)
- [ ] Automate member onboarding
- [ ] Automate secret rotation
- [ ] Set up ACU alerts
- [ ] Create usage dashboards

### Week 9+: Advanced
- [ ] Integrate with security monitoring
- [ ] Implement compliance reporting
- [ ] Optimize ACU allocation
- [ ] Train team admins
- [ ] Establish governance process

---

## 📖 Part 12: Resources

### Official Documentation
- [Devin Enterprise Docs](https://docs.devin.ai/enterprise/overview)
- [Enterprise API v3 Reference](https://docs.devin.ai/api-reference/v3)
- [Release Notes 2026](https://docs.devin.ai/release-notes/2026)
- [Security Best Practices](https://docs.devin.ai/security/overview)

### Community & Support
- [Enterprise Slack Channel](https://app.devin.ai/settings/support)
- [Cognition AI Support](mailto:support@cognition.ai)
- [Mercari Engineering Blog](https://engineering.mercari.com/en/blog/entry/20260403-secure-devin-management/)

### Tools
- **Terraform Provider**: Custom (Mercari's implementation)
- **GitHub Actions**: Automation workflows
- **Google Secret Manager**: Credential storage
- **Cloud Run Job**: Audit log collection

---

## 🎯 Quick Reference

### Admin Checklist (First 30 Days)

```
Week 1:
□ SSO configured
□ First orgs created
□ Initial members added
□ ACU limits set

Week 2:
□ API key policy defined
□ Secret management configured
□ Audit logging enabled
□ MCP allowlist created

Week 3:
□ Terraform/IaC setup
□ Automation workflows created
□ Usage dashboards built
□ Team admins trained

Week 4:
□ First access review completed
□ Incident response tested
□ Documentation finalized
□ Governance process established
```

### Emergency Procedures

```
Compromised API Key:
1. Revoke immediately via API
2. Rotate affected secrets
3. Audit recent session activity
4. Notify security team
5. Document incident

Runaway Session (High ACU):
1. Stop session via admin console
2. Review what caused high usage
3. Adjust session limits if needed
4. Notify user with coaching

Departed Employee:
1. Remove from all orgs immediately
2. Revoke all API keys
3. Review recent session activity
4. Rotate any secrets they accessed
```

---

**Last Updated:** April 13, 2026  
**Author:** weisenaibot 🐺  
**License:** Internal use only  
**Based on:** Official Devin Docs + Mercari Case Study + Cognition AI Announcements
