# Access Review Strategy

## Overview

This document outlines the access review and governance program implemented to ensure users maintain only the access they need (least privilege principle).

---

## Access Review Campaigns

### 1. Quarterly Department Reviews

**Scope:** IT-Department, Finance-Department, HR-Department

**Frequency:** Every 3 months

**Reviewer:** Department managers (Tony Stark for IT, Pepper Potts for Finance)

**Purpose:**
- Verify all group members still need departmental access
- Remove transferred employees who kept old access
- Ensure new hires were properly provisioned

**Auto-remediation:** Enabled - denied access removed immediately

**Compliance requirement:** SOC 2 CC6.2, ISO 27001 A.9.2.1

---

### 2. Quarterly All-Employees Review

**Scope:** All-Employees group (company-wide access)

**Frequency:** Every 3 months

**Reviewer:** Individual managers (each reviews their direct reports)

**Purpose:**
- Identify departed employees still with access
- Catch contractor access that should have expired
- Verify organizational hierarchy is current

**Auto-remediation:** Enabled

**If no response:** Remove access (stricter for company-wide access)

---

### 3. Quarterly Guest User Review

**Scope:** All external users (partners, vendors, contractors)

**Frequency:** Every 3 months (more often than employees)

**Reviewer:** Group owners or security team

**Purpose:**
- Remove contractors whose engagements ended
- Verify partners still need access
- Prevent guest account sprawl

**Auto-remediation:** Enabled

**Additional action:** Guest accounts denied are fully removed from tenant (not just groups)

**Compliance requirement:** External access requires more frequent review per most security frameworks

---

### 4. Monthly Inactive User Detection

**Scope:** All-Employees

**Frequency:** Every month

**Reviewer:** Automated recommendations + manager approval

**Purpose:**
- Detect dormant accounts (security risk)
- Find employees on extended leave
- Identify accounts that should be disabled

**Inactivity threshold:** 30 days without sign-in

**Auto-remediation:** Enabled

**System recommendation:** Auto-deny anyone inactive 30+ days, manager can override if legitimate (approved leave, etc.)

---

## Review Schedule

| Review Name | Frequency | Duration | Next Due | Reviewers |
|------------|-----------|----------|----------|-----------|
| IT Department | Quarterly | 7 days | April 2026 | Tony Stark |
| Finance Department | Quarterly | 7 days | April 2026 | Pepper Potts |
| All Employees | Quarterly | 7 days | April 2026 | Managers |
| Guest Users | Quarterly | 7 days | April 2026 | Security Team |
| Inactive Users | Monthly | 7 days | Feb 2026 | Automated |

---

## Reviewer Responsibilities

**What reviewers must do:**
1. Review all assigned users within 7-day window
2. Verify each user still needs access based on current role
3. Provide business justification for all approvals
4. Deny access for:
   - Transferred employees (no longer in department)
   - Departed employees
   - Inactive accounts (30+ days no sign-in without explanation)
   - Contractors whose engagement ended

**What happens if reviewer doesn't respond:**
- Department reviews: No change (grace period)
- All-Employees review: Access removed automatically
- Guest user review: Guest removed from tenant

---

## Automation & Enforcement

**Auto-apply decisions:** Enabled on all reviews
- When reviewer approves → User keeps access
- When reviewer denies → Access removed within minutes
- No manual IT intervention required

**Benefits:**
- Immediate enforcement (no lag between decision and action)
- Reduces IT workload (no manual group removals)
- Ensures consistency (system enforces, not humans)
- Complete audit trail (all changes logged)

---

## Compliance Mapping

| Framework | Requirement | How We Meet It |
|-----------|------------|----------------|
| **SOC 2 Type II** | CC6.2 - Periodic access reviews | Quarterly reviews of all access |
| **ISO 27001** | A.9.2.5 - Review user access rights | Automated quarterly campaigns |
| **NIST CSF** | PR.AC-4 - Access permissions managed | Manager-driven attestation |
| **GDPR** | Article 32 - Access control | Guest user reviews + removal |

---

## Reporting & Audit Trail

**What gets logged:**
- Who was reviewed
- Who made the decision
- What decision was made (approve/deny)
- Justification provided
- When the decision was made
- Whether access was removed

**Retention:** 7 years minimum for compliance

**Access:** Security team, compliance team, auditors

**Export format:** CSV reports available for all completed reviews

---

## Success Metrics

**Completion rate:** Target 95%+ within 7-day window

**Average review time:** Target <30 seconds per user

**False positives:** Target <5% (approvals that should have been denials)

**Automation rate:** 100% (all decisions auto-applied)

**Compliance:** 0 audit findings related to access reviews

---

## Future Enhancements

**Phase 2 (Months 3-6):**
- Add application-specific access reviews (who has admin rights in which apps)
- Implement risk-based review frequency (high-risk apps reviewed monthly)
- Integration with HRIS (auto-flag terminated employees)

**Phase 3 (Months 6-12):**
- Machine learning recommendations (predict who will need access)
- Self-service attestation (users certify their own access annually)
- Integration with ticketing system (access requests linked to reviews)

---

**Document Version:** 1.0  
**Last Updated:** February 2026  
**Owner:** IT Security & Governance Team  
**Review Frequency:** Quarterly
