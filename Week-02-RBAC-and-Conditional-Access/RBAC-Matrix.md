# RBAC Matrix - Role-Based Access Control

## Role Definitions

| Role | Group | Entra ID Role | Permissions | Use Case |
|------|-------|---------------|-------------|----------|
| Helpdesk Tier 1 | Helpdesk-Tier1 | Helpdesk Administrator | Password resets, unlock accounts | First-level IT support |
| Security Analyst | Security-Analysts | Security Reader | View security logs, read-only access | SOC monitoring |
| IT Administrator | IT-Admins | Global Administrator | Full tenant control | Infrastructure management |

## User Assignments

| User | Department | Groups | Entra Roles | Access Level |
|------|-----------|--------|-------------|--------------|
| Peter Parker | IT | Helpdesk-Tier1, All-Employees | Helpdesk Administrator | Limited admin (password resets) |
| Natasha Romanoff | IT | Security-Analysts, All-Employees | Security Reader | Read-only security access |
| Tony Stark | IT | IT-Admins, IT-Department, All-Employees | Global Administrator | Full administrative control |
| Pepper Potts | Finance | Finance-Department, All-Employees | None | Standard user |

## Principle of Least Privilege

Each role receives only the minimum permissions necessary:
- **Helpdesk:** Cannot modify security settings, only user passwords
- **Security Analyst:** Cannot make changes, only observe
- **IT Admin:** Full control, but policies require compliant devices

## Business Justification

**Helpdesk Administrator Role:**
- Enables Tier 1 support to resolve common issues (password resets, account unlocks)
- Prevents over-privileged access (cannot delete users, modify security settings)
- Reduces dependency on full administrators for routine tasks

**Security Reader Role:**
- Allows SOC analysts to monitor security events and logs
- Read-only access prevents accidental changes during investigations
- Supports compliance requirements for separation of duties

**Global Administrator Role:**
- Reserved for senior IT leadership only
- Full control required for infrastructure changes
- Additional security controls applied (compliant device requirement)

## Access Review Schedule

| Role | Review Frequency | Reviewer |
|------|-----------------|----------|
| Helpdesk Administrator | Quarterly | IT Manager |
| Security Reader | Quarterly | Security Manager |
| Global Administrator | Monthly | CTO/CISO |

---

**Documentation Date:** January 2026  
**Last Review:** January 2026  
**Next Review:** April 2026
