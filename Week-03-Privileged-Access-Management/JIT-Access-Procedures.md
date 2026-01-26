# Just-In-Time Access Procedures

## Overview

This document explains how to request and approve time-limited administrative access using Microsoft Entra ID Privileged Identity Management (PIM). Just-In-Time (JIT) access means admin rights are granted only when needed and automatically expire after a set time.

---

## For Users: How to Activate Admin Roles

### Why JIT Access?

**Traditional approach (risky):**
- You have admin rights 24/7/365
- Even when you're not doing admin work
- If your account gets compromised = instant full access for attackers

**JIT approach (secure):**
- You have zero admin rights by default
- Activate only when you need to do admin tasks
- Rights automatically expire after a few hours
- If compromised during inactive time = no admin access

---

### Step 1: Determine If You Actually Need Admin Access

**Ask yourself:**
- Can I do this without admin rights? (Try first!)
- Is this urgent or can it wait for approval?
- What's the minimum role I need? (Don't activate Global Admin if User Admin works)

**Principle:** Only activate when absolutely necessary. Every activation is logged and reviewed.

---

### Step 2: Request Activation

**Navigate to PIM:**
1. Go to **Azure Portal**: https://portal.azure.com
2. Search for: **Privileged Identity Management** (or just type "PIM")
3. Click **My roles** (left menu)
4. Click **Microsoft Entra roles** tab

**You'll see your eligible roles:**
- Global Administrator
- User Administrator
- Security Administrator
- etc.

**Click "Activate"** next to the role you need.

---

### Step 3: Provide Justification

A form appears asking why you need this access. Be specific!

**✅ Good Justification Examples:**
```
"Emergency: Domain controller offline, restoring from backup"
"Scheduled maintenance: Applying January security patches to Exchange"
"Incident response: Investigating suspected ransomware on file server"
"Ticket #INC-2026-123: User lockout requires admin-level password reset"
"Compliance audit: Need to pull admin access reports for SOC 2"
```

**❌ Bad Justification Examples:**
```
"Need admin access"
"Doing admin stuff"
"Just because"
"Testing"
```

**Pro Tips:**
- Include ticket numbers from your helpdesk system
- Reference specific systems/servers
- Mention if this is scheduled or emergency
- Be honest - auditors review these later

---

### Step 4: Wait for Approval (If Required)

**Some roles require approval, some don't:**

| Role | Approval Required? | Typical Wait Time |
|------|-------------------|-------------------|
| Global Administrator | ✅ Yes | 15-30 minutes |
| Security Administrator | ✅ Yes | 15-30 minutes |
| User Administrator | ❌ No | Instant activation |
| Helpdesk Administrator | ❌ No | Instant activation |

**While waiting:**
- Check PIM dashboard for status: "Pending approval"
- You'll get email/notification when approved or denied
- If urgent, contact your approver directly

**If denied:**
- Read the denial reason
- Fix the issue (better justification, request correct role, etc.)
- Request again

---

### Step 5: Perform Your Admin Tasks

**Once activated:**

✅ **Do:**
- Complete your task efficiently
- Document what you changed (for audit trail)
- Stick to the justification you provided
- Deactivate manually when done (don't wait for expiration)

❌ **Don't:**
- Use the access for unrelated tasks ("While I'm admin, let me also...")
- Share your session with others
- Walk away from your computer while activated
- Forget you're activated (check before leaving for the day)

**Time limits you have:**
- Global Administrator: 4 hours maximum
- User Administrator: 8 hours maximum
- Other roles: Varies (check when you activate)

**⚠️ Warning:** If you don't finish in time, your access expires mid-task. Plan accordingly!

---

### Step 6: Deactivate When Done

**Manual deactivation (recommended):**

1. Go back to **PIM** → **My roles**
2. Click **Active assignments** tab
3. Find your activated role
4. Click **Deactivate**
5. Confirm

**Why deactivate manually?**
- Reduces your attack surface immediately
- Shows good security hygiene to auditors
- Prevents "I forgot I was admin" mistakes

**Auto-deactivation:**
- If you forget, role expires automatically after time limit
- You'll lose access mid-task if you're still working
- Better to deactivate yourself when done

---

## For Approvers: How to Review Activation Requests

### You'll Get a Notification

**Email subject:**
```
[Action Required] Role activation request from Tony Stark
```

**What it includes:**
- Who is requesting
- Which role they want
- How long they need it
- Their justification
- Link to approve/deny

---

### Review the Request

**Navigate to approval queue:**
1. Go to **PIM** → **Approve requests**
2. Click **Microsoft Entra roles** tab
3. You'll see pending requests

**Click on the request to see details:**
- Requestor: Tony Stark
- Role: Global Administrator
- Duration: 4 hours
- Justification: "Emergency infrastructure maintenance..."
- Ticket reference: INC-2026-456

---

### Make Your Decision

**✅ Approve if:**
- Justification is clear and specific
- Request aligns with user's job responsibilities
- Duration is reasonable for the task
- No recent security concerns with this user
- Timing makes sense (emergency at 3 AM = suspicious, scheduled maintenance = fine)

**❌ Deny if:**
- Justification is vague or missing
- User doesn't need this level of access (suggest lower role)
- Duration is excessive ("I need Global Admin for 8 hours" - why?)
- Security concerns (recent suspicious activity, failed phishing test, etc.)
- Better alternative exists (User Admin sufficient, don't need Global)
- Request violates change freeze/maintenance windows

---

### Provide Feedback

**When approving:**
```
✅ "Approved for emergency maintenance window. Please deactivate when complete 
and document all changes in ticket INC-2026-456."
```

**When denying:**
```
❌ "Denied - User Administrator role is sufficient for password resets. 
Please request User Admin instead of Global Admin."
```
```
❌ "Denied - Justification too vague. Please resubmit with specific task 
description and ticket number."
```

**Good feedback helps users:**
- Understand why they were denied
- Learn what info to include next time
- Choose the right role for their task

---

### Approval Best Practices

**Response time targets:**
- Emergency requests: < 30 minutes
- Scheduled requests: < 4 hours
- After-hours: Check phone for urgent notifications

**Questions to ask yourself:**
- Would I grant this access if it were permanent? (If no, probably deny)
- Is this the minimum role needed? (Suggest lower if possible)
- Does the timing make sense? (Saturday 3 AM admin request = suspicious)
- Has this user had recent security issues? (Failed phishing test, weak password)

**Document your reasoning:**
Every approval/denial is logged. If auditors ask "Why did you approve Global Admin at 3 AM?" you should have a good answer.

---

## Emergency Procedures

### What If PIM Is Down?

**Break-Glass Emergency Account:**

**When to use:**
- PIM service completely unavailable
- Identity service outage
- Critical emergency requiring immediate admin access
- Approver unreachable during critical incident

**Break-glass account details:**
- Account name: `breakglass-admin@company.com`
- Credentials: Stored in physical safe (IT Director's office)
- **Permanent Global Administrator** (not PIM-managed)
- Excluded from all Conditional Access policies
- Excluded from MFA requirements

**⚠️ Break-glass usage triggers:**
- Immediate alert to security team
- CEO/CISO notification
- Incident investigation automatically opened
- Full audit of all actions taken

**After using break-glass:**
1. Document reason for use in incident ticket
2. List all actions taken while using account
3. Rotate credentials immediately
4. Security team reviews all actions
5. Root cause analysis: Why was PIM unavailable?

---

### Escalation Contacts

**If you can't get admin access when needed:**

| Issue | Contact | Response Time |
|-------|---------|---------------|
| PIM not working | IT Service Desk | 15 minutes |
| Approver not responding | Backup approver (list in runbook) | 30 minutes |
| Emergency after-hours | On-call admin (PagerDuty) | 15 minutes |
| Break-glass needed | IT Director + Security Team | Immediate |

---

## Role-Specific Guidelines

### Global Administrator

**Who should request:** IT Directors, Senior Infrastructure Engineers  
**Approval required:** ✅ Yes (always)  
**Max duration:** 4 hours  
**When needed:** Tenant-wide changes, emergency response, compliance audits

**Common valid uses:**
- Emergency infrastructure repairs
- Tenant configuration changes
- Disaster recovery operations
- Security incident response (confirmed breach)

**Red flags:**
- Requested for routine tasks
- Vague justification
- Unusual timing (middle of night without emergency)

---

### User Administrator

**Who should request:** Helpdesk leads, IT support staff  
**Approval required:** ❌ No (activates immediately)  
**Max duration:** 8 hours  
**When needed:** User management, group management, license assignments

**Common valid uses:**
- Bulk user onboarding (new department)
- Group membership updates
- License assignment corrections
- User account troubleshooting

**Tip:** This role covers 80% of daily admin tasks. Use this instead of Global Admin whenever possible.

---

### Helpdesk Administrator

**Who should request:** Tier 1 support staff  
**Approval required:** ❌ No  
**Max duration:** 8 hours  
**When needed:** Password resets, account unlocks, basic troubleshooting

**Note:** This role is often assigned permanently (not via PIM) since it's low-risk and needed constantly for support work.

---

## Audit & Compliance

### What Gets Logged

Every PIM action is logged:
- ✅ Who requested access
- ✅ Which role
- ✅ When they requested
- ✅ Justification provided
- ✅ Who approved/denied
- ✅ Approval reasoning
- ✅ When access was activated
- ✅ When access expired or was deactivated
- ✅ What actions were taken while activated (in separate audit logs)

**Retention:** 90 days in PIM, 7 years in compliance archive

---

### Periodic Access Reviews

**Quarterly reviews check:**
- Does this person still need eligible access to this role?
- Has their job changed?
- Any security incidents involving this user?
- Excessive activation frequency? (Sign of role creep)

**If access is denied in review:**
- Eligible assignment removed automatically
- User notified via email
- Manager notified
- Can request reinstatement with business justification

---

## Common Questions

**Q: Can I activate multiple roles at once?**  
A: Yes, but only activate what you need. Each role activation is logged separately.

**Q: What if I need more than 4 hours for a big project?**  
A: Break it into phases. Activate for 4 hours, complete a chunk, deactivate. Activate again later for next chunk.

**Q: Can someone else activate admin access for me?**  
A: No. PIM requires you to activate your own eligible roles. This ensures accountability.

**Q: What if I'm denied and disagree?**  
A: Talk to your approver. If still denied, escalate to IT Director with business justification.

**Q: Does PIM work offline?**  
A: No. PIM requires internet connectivity to Azure. For on-prem emergencies, use break-glass account.

**Q: Can I activate a role "just in case" I need it later?**  
A: No. Activate only when you have a specific task requiring admin access right now.

---

## Tips for Success

**For requestors:**
1. Always try to complete tasks without admin access first
2. Request the lowest-privilege role that works
3. Include ticket numbers in justifications
4. Deactivate as soon as you're done
5. Document what you changed

**For approvers:**
1. Respond quickly (people are often waiting to fix urgent issues)
2. Provide helpful feedback when denying
3. Suggest alternative roles if applicable
4. Trust but verify - approve legitimate requests, deny suspicious ones
5. Remember: Denying is okay if request doesn't make sense

---

**Document Version:** 1.0  
**Last Updated:** January 2026  
**Owner:** IT Security Team  
**Review Frequency:** Quarterly
