# Privileged Identity Management (PIM) Configuration

## Overview

This document details the Just-In-Time (JIT) privileged access configuration implemented using Microsoft Entra ID Privileged Identity Management.

---

## Configured Roles

### Global Administrator
**Eligible Users:** Tony Stark

**Activation Requirements:**
- Azure MFA verification required
- Business justification required
- Approval required (approver: Admin account)
- Maximum duration: 4 hours
- Auto-expires after time limit

**Use Case:** 
Emergency infrastructure maintenance, critical system changes, tenant-wide configuration

---

### User Administrator
**Eligible Users:** Peter Parker

**Activation Requirements:**
- Azure MFA verification required
- Business justification required
- No approval required (lower risk role)
- Maximum duration: 8 hours
- Auto-expires after time limit

**Use Case:**
User account management, password resets, license assignments, group management

---

## Approval Workflow

**For Global Administrator:**
1. User requests activation via PIM
2. Request includes justification and duration
3. Approval notification sent to designated approver
4. Approver reviews justification
5. If approved: Role activated for specified duration
6. If denied: User notified, must request again with better justification

**Approval SLA:** 30 minutes during business hours

---

## Security Benefits

**Before PIM (Traditional Approach):**
- Tony had permanent Global Administrator rights
- 24/7/365 admin access (even when not needed)
- If account compromised = immediate full tenant access
- No automatic expiration
- No approval required

**After PIM (Just-In-Time Access):**
- Tony has zero admin rights by default
- Must activate when needed (friction by design)
- If compromised during inactive period = no admin access
- Automatically expires after 4 hours
- Requires approval for activation
- Every activation logged for audit

**Risk Reduction:** ~95% reduction in attack surface

---

## Access Review Schedule

**Frequency:** Quarterly  
**Scope:** All eligible and active admin role assignments  
**Reviewer:** IT Security Lead  
**Auto-remediation:** Enabled (denied access removed automatically)  

**Review Checklist:**
- Does user still need this role?
- Has user's job function changed?
- Any security incidents involving this user?
- Alternative least-privilege options available?

---

**Document Version:** 1.0  
**Last Updated:** January 2026  
**Next Review:** April 2026
