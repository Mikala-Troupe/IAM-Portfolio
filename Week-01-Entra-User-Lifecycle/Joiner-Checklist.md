# Joiner (New Employee Onboarding) Checklist

## Employee Information
- **Name:** Peter Parker
- **Email:** peter.parker@[yourdomain].onmicrosoft.com
- **Job Title:** IT Support Specialist
- **Department:** IT
- **Start Date:** January 19, 2026
- **Manager:** Tony Stark (IT Director)
- **Employee Type:** Full-time

---

## Provisioning Steps Completed

### Account Creation
- [x] User account created in Microsoft Entra ID
- [x] User Principal Name (UPN) configured
- [x] Display name set correctly
- [x] Temporary password generated
- [x] Password change required on first login

### Profile Configuration
- [x] First name: Peter
- [x] Last name: Parker
- [x] Job title: IT Support Specialist
- [x] Department: IT
- [x] Manager relationship: Tony Stark
- [x] Usage location set (required for licensing)
- [x] Company name added

### Access Provisioning
- [x] Added to **All-Employees** security group
- [x] Added to **IT-Department** security group
- [x] Verified group memberships applied correctly
- [x] Baseline access permissions granted

### Security & Compliance
- [x] Account enabled and active
- [x] No admin roles assigned (least privilege)
- [x] User type set to "Member" (not Guest)
- [x] Account creation documented in Entra ID audit logs

---

## Access Granted

### Security Groups
| Group Name | Purpose | Access Level |
|-----------|---------|--------------|
| All-Employees | Company-wide resources | Read access to shared resources |
| IT-Department | IT team resources | Access to IT systems and tools |

### Expected Application Access
(Based on group memberships - would auto-provision in production)
- Microsoft 365 applications (Outlook, Teams, SharePoint)
- IT ticketing system (ServiceNow)
- IT documentation (Confluence/SharePoint)
- Company intranet

---

## Verification Steps

- [x] User account visible in Entra ID user list
- [x] Profile information accurate and complete
- [x] Group memberships showing correctly
- [x] Manager relationship established (reports to Tony Stark)
- [x] Account status: Enabled
- [x] Sign-in allowed: Yes

---

## Post-Provisioning Tasks

### Immediate (Day 0)
- [x] Credentials prepared for delivery
- [x] Welcome email drafted (would be sent to Tony Stark)
- [x] IT onboarding ticket created (simulated)

### Day 1
- [ ] Peter successfully logs in and changes password
- [ ] MFA enrollment completed (Week 2 lab)
- [ ] Access to required applications verified
- [ ] Tony Stark confirms Peter is productive

### Week 1
- [ ] Peter completes security awareness training
- [ ] Additional role-specific access requested if needed
- [ ] IT verifies no access issues reported

---

## Notes

**Security Considerations:**
- Temporary password set with forced change on first login to prevent credential exposure
- No administrative privileges assigned - adheres to least privilege principle
- Account enabled only after manager approval (simulated)

**Business Impact:**
- Peter can be productive immediately on Day 1
- IT department access grants tools needed for support role
- Manager relationship enables org chart accuracy (Peter → Tony Stark → CTO)

**Compliance:**
- All provisioning actions logged in Entra ID audit trail
- Group-based access simplifies future access reviews
- Documentation supports SOX/HIPAA compliance requirements

**Next Steps:**
- Week 2 lab will add Conditional Access and MFA requirements
- Future enhancements: integrate with HRIS for automated provisioning
- Consider role-based access templates for faster onboarding

---

**Provisioned By:** Mikala Troupe  
**Date:** January 19, 2026  
**Verification:** Complete ✅
