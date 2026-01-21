# Mover (Internal Transfer) Checklist

## Transfer Information

### Employee Details
- **Employee Name:** Peter Parker
- **Employee Email:** peter.parker@datgirlace2020gmail.onmicrosoft.com
- **Transfer Date:** January 19, 2026
- **Transfer Type:** Departmental transfer

### Previous Role
- **Department:** IT
- **Job Title:** IT Support Specialist
- **Manager:** Tony Stark (IT Director)
- **Primary Security Group:** IT-Department

### New Role
- **Department:** Finance
- **Job Title:** Financial Analyst
- **Manager:** Pepper Potts (Finance Director)
- **Primary Security Group:** Finance-Department

---

## Changes Performed

### Profile Updates
- [x] Job title updated: IT Support Specialist → Financial Analyst
- [x] Department changed: IT → Finance
- [x] Manager reassigned: Tony Stark → Pepper Potts
- [x] Profile changes saved and verified

### Group Membership Changes
- [x] **Removed** from IT-Department security group
- [x] **Added** to Finance-Department security group
- [x] Retained membership in All-Employees group
- [x] Group changes verified in user profile

### Verification
- [x] User profile reflects new role information
- [x] New manager relationship visible in org chart (Peter → Pepper Potts)
- [x] Group memberships accurately show new department
- [x] Old department access removed
- [x] New department access granted

---

## Access Impact Analysis

### Access Removed
| Resource | Group | Impact |
|----------|-------|--------|
| IT Systems | IT-Department | No longer has access to IT-specific tools |
| IT Documentation | IT-Department | SharePoint/Confluence IT folders revoked |
| IT Ticketing Admin | IT-Department | ServiceNow elevated permissions removed |

### Access Granted
| Resource | Group | Impact |
|----------|-------|--------|
| Finance Systems | Finance-Department | ERP/accounting system access granted |
| Financial Reports | Finance-Department | Power BI finance dashboards accessible |
| Budget Tools | Finance-Department | Financial planning applications available |

### Access Unchanged
| Resource | Group | Impact |
|----------|-------|--------|
| Microsoft 365 | All-Employees | Email, Teams, OneDrive remain accessible |
| Company Intranet | All-Employees | Internal communication platform unchanged |
| HR Self-Service | All-Employees | Benefits and payroll portals still available |

---

## Communication & Notifications

### Notifications Sent (Production Scenario)
- [ ] **Previous Manager (Tony Stark):** Notified of Peter's transfer, access changes
- [ ] **New Manager (Pepper Potts):** Notified of new team member, access granted
- [ ] **IT Department:** Peter removed from department distribution lists
- [ ] **Finance Department:** Peter added to department distribution lists
- [ ] **Employee (Peter Parker):** Informed of access changes and new resources available

---

## Compliance & Audit

### Documentation
- [x] Before-state screenshot captured (IT role)
- [x] After-state screenshot captured (Finance role)
- [x] Group membership changes logged in Entra ID
- [x] Transfer effective date documented
- [x] Manager approval obtained (simulated)

### Audit Trail
- All changes tracked in Microsoft Entra ID audit logs
- Transfer date: January 19, 2026
- Modified by: Mikala Troupe (IAM Administrator)
- Approval reference: Manager approval from Tony Stark (simulated)

---

## Post-Transfer Verification

### Immediate (Day 0)
- [x] Profile updates successful
- [x] Group changes applied
- [x] No errors in provisioning logs

### Day 1
- [ ] Peter successfully accesses Finance systems
- [ ] Peter confirms IT access appropriately removed
- [ ] Pepper Potts confirms Peter has correct access
- [ ] No help desk tickets for access issues

### Week 1
- [ ] Peter completes Finance department onboarding
- [ ] Access to all necessary Finance tools verified
- [ ] Any additional role-specific access requested and provisioned

---

## Notes

**Process Efficiency:**
- Manual transfer completed in ~3 minutes
- In production with automated provisioning: < 30 seconds
- Zero downtime - Peter maintains access to core systems throughout

**Security Considerations:**
- Old department access removed immediately to prevent privilege creep
- New access granted based on role requirements only
- Least privilege maintained throughout transfer
- Manager approval ensures proper authorization

**Business Impact:**
- Seamless transition minimizes productivity loss
- Immediate access to Finance tools enables Day 1 effectiveness
- Automated group-based provisioning would scale to 100s of transfers

**Lessons Learned:**
- Group-based access makes transfers simple and auditable
- Clear role definitions enable predictable access patterns
- Documentation critical for compliance and troubleshooting

**Future Improvements:**
- Integrate with HRIS to trigger transfers automatically
- Implement approval workflows for manager sign-off
- Auto-notify affected parties (Tony Stark, Pepper Potts, Peter)
- Create role-based access templates for common transfers

---

**Transfer Processed By:** Mikala Troupe  
**Date:** January 20, 2026  
**Status:** Complete ✅  
**Verification:** All access changes confirmed
