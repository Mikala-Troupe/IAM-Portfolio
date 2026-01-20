# Leaver (Employee Offboarding) Checklist

## Departure Information

### Employee Details
- **Name:** Alex Johnson
- **Email:** alex.johnson@[yourdomain].onmicrosoft.com
- **Job Title:** Financial Analyst
- **Department:** Finance
- **Manager:** Michael Finance
- **Last Working Day:** January 19, 2026
- **Reason for Departure:** Resignation
- **Notice Period:** 2 weeks (standard)

---

## Pre-Offboarding Actions

### Information Gathering
- [x] Departure date confirmed with HR
- [x] Manager approval for offboarding obtained
- [x] Exit interview scheduled (simulated)
- [x] Knowledge transfer status checked

### Access Documentation
- [x] Current group memberships exported to CSV
- [x] Application access audit completed
- [x] Active sessions reviewed in sign-in logs
- [x] Recent account activity documented
- [x] Devices assigned to user identified (N/A for lab)

### Data & Assets
- [x] User's OneDrive/SharePoint content reviewed
- [x] Email forwarding requirements determined (if any)
- [x] Company devices return scheduled (N/A for lab)
- [x] Access credentials inventory completed

---

## Offboarding Steps Completed

### Account Deactivation
- [x] User account **disabled** in Microsoft Entra ID
- [x] Account status changed to "Disabled" (not deleted)
- [x] Sign-in blocked immediately
- [x] Multi-factor authentication (MFA) disabled
- [x] Account disable timestamp documented

### Access Revocation
- [x] **Removed** from Finance-Department security group
- [x] **Removed** from All-Employees security group
- [x] Verified all group memberships removed
- [x] Application access revoked via group removal
- [x] Shared mailbox permissions removed (if applicable)

### Profile Updates
- [x] Offboarding notes added to user profile
- [x] Departure reason documented
- [x] Last working day recorded
- [x] Manager notified of account deactivation

### Audit & Compliance
- [x] Sign-in logs exported for last 30 days
- [x] Group membership export retained for audit
- [x] Screenshots of disabled account captured
- [x] Offboarding actions logged in Entra ID
- [x] Retention policy applied (90-day hold before deletion)

---

## Access Revoked

### Security Groups Removed
| Group Name | Access Lost | Revocation Time |
|-----------|-------------|-----------------|
| Finance-Department | Finance systems, financial reports, budget tools | Immediate |
| All-Employees | Microsoft 365, company intranet, HR portal | Immediate |

### Application Access Revoked
(Auto-revoked via group membership removal in production)
- ❌ Microsoft 365 (Outlook, Teams, OneDrive, SharePoint)
- ❌ Finance ERP systems
- ❌ Power BI financial dashboards
- ❌ Company intranet
- ❌ HR self-service portal
- ❌ Any SSO-connected applications

### Credentials Invalidated
- ❌ All active sessions terminated
- ❌ Refresh tokens revoked
- ❌ Application passwords disabled
- ❌ API access keys invalidated (if any)

---

## Data Retention & Cleanup

### Immediate (Day 0)
- [x] Account disabled to prevent further access
- [x] Active sessions terminated
- [x] Group memberships removed
- [x] Manager and HR notified

### 30-Day Retention Period
- [ ] Email forwarding configured to manager (if requested)
- [ ] OneDrive access granted to manager for data retrieval
- [ ] Shared files ownership transferred
- [ ] Distribution list memberships reviewed and updated

### 90-Day Retention Period
- [ ] Account remains disabled but not deleted
- [ ] Audit logs retained for compliance
- [ ] Legal hold assessed (none required for this user)
- [ ] Data deletion impact analysis completed

### Post-90 Days
- [ ] Account permanently deleted (if no legal hold)
- [ ] Associated data removed per retention policy
- [ ] Licenses reclaimed and reassigned
- [ ] Final offboarding report archived

---

## Verification & Quality Checks

### Immediate Verification
- [x] User account status shows "Disabled"
- [x] All group memberships successfully removed
- [x] Sign-in logs confirm no activity post-disable
- [x] Entra ID audit logs show offboarding actions

### Follow-Up Verification
- [ ] No help desk tickets from user (access properly blocked)
- [ ] Manager confirms data transfer complete
- [ ] Finance team confirms no access issues
- [ ] IT confirms no orphaned resources

---

## Compliance & Audit Trail

### Documentation Retained
| Document | Purpose | Retention Period |
|----------|---------|------------------|
| Group membership export | Compliance audit | 7 years |
| Sign-in logs | Security forensics | 90 days |
| Offboarding approval | HR record | Permanent |
| Account disable screenshot | Verification | 7 years |

### Regulatory Compliance
- ✅ **SOX Compliance:** User access removed within 24 hours of termination
- ✅ **HIPAA (if applicable):** PHI access revoked immediately
- ✅ **GDPR (if applicable):** Data retention policy applied
- ✅ **Company Policy:** 90-day retention before deletion

---

## Security Incident Check

### Suspicious Activity Review
- [x] No unusual sign-in locations detected
- [x] No abnormal access patterns in final 30 days
- [x] No bulk data downloads flagged
- [x] No privilege escalation attempts
- [x] No security alerts associated with this user

**Conclusion:** Clean offboarding - no security concerns identified

---

## Notifications Sent

### Internal Stakeholders
- [x] **Manager (Michael Finance):** User access terminated, data transfer options
- [x] **HR Department:** Offboarding complete, final payroll can proceed
- [x] **IT Security:** Account disabled, monitor for any breach attempts
- [x] **Finance Team:** Distribution lists updated, access revoked

### External (if applicable)
- [ ] **Clients/Partners:** Informed of new point of contact (if user-facing role)
- [ ] **Vendors:** Access to third-party systems revoked

---

## Post-Offboarding Tasks

### Immediate
- [x] Access terminated
- [x] Manager notified
- [x] Audit trail documented

### Week 1
- [ ] Verify no access restoration requests
- [ ] Monitor for any unauthorized access attempts
- [ ] Confirm email forwarding working (if configured)

### Month 1
- [ ] Review OneDrive data transfer completion
- [ ] Reclaim Microsoft 365 license
- [ ] Archive or transfer shared files

### Month 3
- [ ] Confirm legal hold not required
- [ ] Schedule account for permanent deletion
- [ ] Final offboarding report to HR

---

## Notes

**Security Best Practices Applied:**
- Account disabled immediately (not deleted) to maintain audit trail
- All access revoked in single operation via group removal
- Session tokens invalidated to prevent cached access
- Comprehensive documentation for compliance and forensics

**Business Continuity:**
- Manager has 30 days to retrieve necessary files
- Email forwarding prevents communication gaps
- Knowledge transfer completed before departure date
- No disruption to Finance team operations

**Lessons Learned:**
- Group-based access made revocation instantaneous and complete
- Documentation critical for audit and potential rehire scenarios
- Automated workflows would further reduce manual effort
- Clear retention policies prevent compliance issues

**Risk Mitigation:**
- Immediate access removal prevents insider threat window
- Audit trail supports investigation if needed
- Proper data handling protects company IP
- Compliance documentation prevents regulatory penalties

**Future Improvements:**
- Integrate with HRIS for automated offboarding triggers
- Implement pre-departure access reviews (7 days before last day)
- Auto-notify all stakeholders via workflow
- Schedule automated license reclamation
- Create executive dashboard for offboarding metrics

---

**Offboarding Processed By:** Mikala Troupe  
**Date:** January 19, 2026  
**Status:** Complete ✅  
**Account State:** Disabled, pending 90-day retention  
**Compliance:** All requirements met  
**Security:** No concerns identified
```

---

## ✅ What You Have Now

After creating these 4 files in Obsidian, your Week 1 folder will have:
```
Week-01-Entra-User-Lifecycle/
├── README.md                ✅ Main portfolio piece
├── Joiner-Checklist.md      ✅ Onboarding documentation
├── Mover-Checklist.md       ✅ Transfer documentation
├── Leaver-Checklist.md      ✅ Offboarding documentation
└── screenshots/             📸 Add your images here
