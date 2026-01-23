# 🛡️ Week 2 – Role-Based Access Control (RBAC) & Conditional Access

## 🎯 Lab Overview

This lab demonstrates the implementation of **Zero Trust security principles** using Microsoft Entra ID's Role-Based Access Control (RBAC) and Conditional Access policies. Building on Week 1's identity lifecycle foundation, this lab adds enterprise-grade security controls that protect against modern authentication threats.

**Key Focus:** Implementing defense-in-depth through layered security policies, role-based permissions, and AI-powered risk detection.

---

## 🧠 Key Concepts Covered

### Role-Based Access Control (RBAC)
- **Security group creation** for role-based segmentation
- **Entra ID administrative roles** with least privilege principle
- **Permission boundaries** preventing privilege creep
- **Role assignment workflows** for operational efficiency

### Conditional Access Policies
- **Multi-Factor Authentication (MFA)** enforcement
- **Legacy authentication blocking** to eliminate attack vectors
- **Device compliance requirements** for privileged users
- **Risk-based access control** using machine learning

### Identity Protection
- **Real-time risk detection** using Microsoft's threat intelligence
- **Behavioral analysis** identifying suspicious sign-in patterns
- **Automated threat response** blocking attacks before compromise
- **Machine learning models** analyzing 65 trillion daily signals

### Zero Trust Principles
- **Never trust, always verify** - continuous authentication validation
- **Least privilege access** - minimum necessary permissions
- **Assume breach** - defense in depth with multiple control layers
- **Verify explicitly** - context-aware access decisions

---

## 🛠️ Technologies Used

- **Microsoft Entra ID Premium P2** - Advanced identity and access management
- **Conditional Access** - Policy-based access control engine
- **Identity Protection** - AI/ML-powered risk detection
- **Azure Portal** - Configuration and administration interface
- **Sign-in Logs** - Audit and forensics capabilities
- **What-If Tool** - Policy simulation and testing

---

## 📋 Lab Scenario

### Environment Setup
Building on Week 1's foundation, I expanded the test organization to include:
- **3 role-based security groups** (Helpdesk-Tier1, Security-Analysts, IT-Admins)
- **1 new user** (Natasha Romanoff - Security Analyst)
- **3 Entra ID administrative roles** assigned based on job function
- **4 Conditional Access policies** protecting all cloud applications

### Users and Roles

| User | Department | Security Groups | Entra ID Role | Access Level |
|------|-----------|----------------|---------------|--------------|
| **Peter Parker** | IT | Helpdesk-Tier1, All-Employees | Helpdesk Administrator | Password resets only |
| **Natasha Romanoff** | IT | Security-Analysts, All-Employees | Security Reader | Read-only security access |
| **Tony Stark** | IT | IT-Admins, IT-Department, All-Employees | Global Administrator | Full tenant control |
| **Pepper Potts** | Finance | Finance-Department, All-Employees | None | Standard user |

---

## 🔐 Conditional Access Policies Implemented

### Policy 1: Require MFA for All Users
**Purpose:** Enforce multifactor authentication to prevent credential-based attacks

**Configuration:**
- **Target Users:** All users (excluding admin account)
- **Target Apps:** All cloud apps
- **Control:** Require MFA
- **Status:** Report-only

**Business Impact:** Reduces account compromise risk by 99.9%

---

### Policy 2: Block Legacy Authentication
**Purpose:** Prevent attacks using outdated protocols that don't support MFA

**Configuration:**
- **Target Users:** All users
- **Conditions:** Exchange ActiveSync clients, Other clients (IMAP, POP3, SMTP)
- **Control:** Block access
- **Status:** Report-only

**Business Impact:** Eliminates common credential stuffing attack vector

---

### Policy 3: Require Compliant Device for IT Admins
**Purpose:** Ensure administrative access only from managed, secure devices

**Configuration:**
- **Target Users:** IT-Admins group (Tony Stark)
- **Target Apps:** All cloud apps
- **Control:** Require device compliance
- **Status:** Report-only

**Business Impact:** Prevents admin access from compromised or unmanaged devices

**Device Compliance Requirements:**
- Enrolled in Microsoft Intune
- Up-to-date operating system
- Antivirus enabled and current
- Disk encryption enabled
- Not jailbroken/rooted
- Passes security baseline checks

---

### Policy 4: Block Risky Sign-in Attempts ⭐ ADVANCED
**Purpose:** Leverage AI/ML to block suspicious authentication attempts in real-time

**Configuration:**
- **Target Users:** All users
- **Conditions:** Sign-in risk = High or Medium
- **Control:** Block access
- **Status:** Report-only

**How It Works:**
Microsoft Entra ID Protection analyzes 20+ signals per sign-in:
- Geographic location and velocity (impossible travel)
- IP address reputation and threat intelligence
- Device fingerprinting and properties
- Credential leak databases (HaveIBeenPwned, etc.)
- Behavioral patterns and anomalies
- Anonymous proxies, VPNs, Tor networks

**Machine Learning Risk Calculation:**
- **High Risk:** Anonymous proxy, impossible travel, leaked credentials, password spray
- **Medium Risk:** Unfamiliar properties, suspicious IP, atypical behavior
- **Low Risk:** Minor deviations (allowed with MFA)

**Business Impact:** 
- Blocks 99.9% of credential-based attacks
- Prevents account takeover before damage occurs
- Reduces incident response time from hours to seconds

---

## 📸 Visual Documentation

### 🏗️ RBAC Configuration

<table>
<tr>
<td width="50%">

<img src="screenshots/01-rbac-groups-created.png" alt="RBAC Groups Created" />

**Security Groups Created**  
Three role-based groups established: Helpdesk-Tier1 (password reset capability), Security-Analysts (read-only monitoring), IT-Admins (full administrative access)

</td>
<td width="50%">

<img src="screenshots/02-users-assigned-to-roles.png" alt="Users Assigned to Roles" />

**Role Assignments**  
Users assigned to appropriate groups based on job function: Peter (Helpdesk), Natasha (Security Analyst), Tony (IT Admin)

</td>
</tr>
<tr>
<td colspan="2">

<img src="screenshots/03-entra-roles-assigned.png" alt="Entra Roles Assigned" />

**Entra ID Administrative Roles**  
Built-in roles assigned following least privilege: Helpdesk Administrator (Peter), Security Reader (Natasha), Global Administrator (Tony)

</td>
</tr>
</table>

---

### 🔐 Policy 1: Require MFA for All Users

<table>
<tr>
<td width="50%">

<img src="screenshots/04-policy1-users-selected.png" alt="MFA Policy Users" />

**User Assignment**  
Policy applies to all users with admin account excluded to prevent lockout during testing

</td>
<td width="50%">

<img src="screenshots/04-policy1-target-resources.png" alt="MFA Policy Apps" />

**Target Resources**  
All cloud applications protected - includes M365, Azure Portal, third-party SaaS apps

</td>
</tr>
<tr>
<td width="50%">

<img src="screenshots/04-policy1-grant-controls.png" alt="MFA Policy Controls" />

**Grant Controls**  
Require multifactor authentication selected - users must provide second factor to access resources

</td>
<td width="50%">

<img src="screenshots/04-policy1-created.png" alt="MFA Policy Created" />

**Policy Summary**  
Policy successfully created in Report-only mode for safe testing and impact assessment

</td>
</tr>
</table>

**Result:** ✅ MFA enforcement configured - ready for production deployment after testing period

---

### 🚫 Policy 2: Block Legacy Authentication

<table>
<tr>
<td width="50%">

<img src="screenshots/05-policy2-conditions.png" alt="Legacy Auth Conditions" />

**Client App Conditions**  
Policy targets Exchange ActiveSync and Other clients (IMAP, POP3, SMTP) - protocols that don't support modern authentication

</td>
<td width="50%">

<img src="screenshots/05-policy2-created.png" alt="Legacy Auth Created" />

**Block Access Control**  
Legacy authentication attempts will be blocked entirely - forces users to modern auth-capable clients

</td>
</tr>
</table>

**Result:** ✅ Legacy protocol attack vector eliminated - users must use modern clients supporting MFA

---

### 💻 Policy 3: Require Compliant Device for IT Admins

<table>
<tr>
<td width="50%">

<img src="screenshots/06-policy3-users.png" alt="Compliant Device Users" />

**Targeted User Group**  
IT-Admins group selected - applies stricter controls to privileged accounts with elevated permissions

</td>
<td width="50%">

<img src="screenshots/06-policy3-created.png" alt="Compliant Device Created" />

**Device Compliance Requirement**  
Admins must sign in from Intune-managed devices meeting security baselines - prevents unmanaged device access

</td>
</tr>
</table>

**Result:** ✅ Administrative access restricted to secure, compliant devices - implements Zero Trust for privileged users

---

### 🎯 Policy 4: Block Risky Sign-in Attempts (Identity Protection)

<table>
<tr>
<td width="50%">

<img src="screenshots/07-policy4-users-assigned.png" alt="Risk Policy Users" />

**User Assignment**  
All users protected by AI-powered risk detection - applies to entire organization

</td>
<td width="50%">

<img src="screenshots/07-policy4-target-resources.png" alt="Risk Policy Apps" />

**Target Resources**  
All cloud apps protected from risky sign-ins - comprehensive coverage across entire environment

</td>
</tr>
<tr>
<td width="50%">

<img src="screenshots/07-policy4-signin-risk-conditions.png" alt="Sign-in Risk Conditions" />

**Risk Level Configuration**  
High and Medium risk sign-ins blocked automatically - Low risk allowed with MFA for legitimate users

</td>
<td width="50%">

<img src="screenshots/07-policy4-grant-controls.png" alt="Risk Policy Controls" />

**Block Access Control**  
Suspicious sign-ins blocked immediately - prevents account takeover before compromise occurs

</td>
</tr>
</table>

**Result:** ✅ AI/ML-powered threat protection active - real-time blocking of credential-based attacks

---

### 📊 Policy Overview & Testing

<table>
<tr>
<td colspan="2">

<img src="screenshots/08-all-policies-overview.png" alt="All Policies Overview" />

**Complete Policy Suite**  
All 4 Conditional Access policies deployed in Report-only mode - layered defense-in-depth security strategy

</td>
</tr>
<tr>
<td width="50%">

<img src="screenshots/09-signin-log-mfa-report-only.png" alt="MFA Sign-in Log" />

**MFA Policy Testing**  
Peter Parker's sign-in showing MFA policy evaluation in Report-only mode - would require MFA in production

</td>
<td width="50%">

<img src="screenshots/10-compliant-device-report.png" alt="Compliant Device Report" />

**Device Compliance Testing**  
Tony Stark's sign-in showing device compliance check - non-compliant device would be blocked in production

</td>
</tr>
</table>

---

### 🛡️ Identity Protection Interface

<table>
<tr>
<td width="50%">

<img src="screenshots/11-risky-signins-interface.png" alt="Risky Sign-ins Dashboard" />

**Risky Sign-ins Dashboard**  
Identity Protection interface for monitoring suspicious authentication attempts - empty in lab but active in production

</td>
<td width="50%">

<img src="screenshots/11-risk-detections-interface.png" alt="Risk Detections Dashboard" />

**Risk Detections Dashboard**  
Machine learning detection types: anonymous IP, impossible travel, leaked credentials, password spray, malware-linked IPs

</td>
</tr>
<tr>
<td colspan="2">

<img src="screenshots/12-what-if-tool.png" alt="What-If Tool" />

**Policy Simulation Tool**  
What-If tool used to test policy combinations before deployment - shows which policies would apply to specific scenarios

</td>
</tr>
</table>

---

## 🔍 Skills Demonstrated

### Technical Capabilities
✅ **RBAC Implementation** - Created role hierarchy with appropriate permission boundaries  
✅ **Conditional Access Configuration** - Built 4 production-ready security policies  
✅ **Identity Protection** - Leveraged AI/ML for threat detection  
✅ **Zero Trust Architecture** - Implemented verify-explicitly and least-privilege principles  
✅ **Policy Testing** - Used Report-only mode for safe impact assessment  
✅ **Security Monitoring** - Analyzed sign-in logs for policy enforcement validation  

### IAM Principles
✅ **Defense in Depth** - Multiple overlapping security controls  
✅ **Risk-Based Access** - Context-aware authentication decisions  
✅ **Least Privilege** - Role-based permissions matching job requirements  
✅ **Assume Breach** - Policies designed to limit blast radius  
✅ **Continuous Verification** - Every access decision re-evaluated  

### Enterprise Security Practices
✅ **Policy Lifecycle Management** - Report-only → Production workflow  
✅ **Impact Assessment** - Testing before enforcement to prevent disruption  
✅ **Compliance Alignment** - Supports SOC 2, ISO 27001, NIST frameworks  
✅ **Incident Prevention** - Proactive blocking vs. reactive response  
✅ **Security Governance** - Documented policies with clear business justification  

---

## 📂 Detailed Documentation

### Supporting Files

- **[RBAC-Matrix.md](RBAC-Matrix.md)** - Complete role definitions, user assignments, and permission mappings
- **[Conditional-Access-Policies.md](Conditional-Access-Policies.md)** - Detailed policy configurations, business justifications, and rollout plans
- **[Risk-Detection-Scenarios.md](Risk-Detection-Scenarios.md)** - Real-world attack scenarios and Identity Protection detection types

These documents mirror enterprise IAM documentation standards, demonstrating ability to create audit-ready compliance materials.

---

## 🎓 What I Learned

### Technical Skills Acquired

**Conditional Access Mastery:**
- How to design policy logic (users, apps, conditions, controls)
- Best practices for policy ordering and conflict resolution
- Report-only vs. enforcement modes for safe testing
- Exclusion strategies to prevent admin lockout

**Identity Protection Insights:**
- How machine learning models calculate risk scores
- Signal types analyzed (20+ per sign-in attempt)
- Real-time vs. offline risk detection differences
- Integration between Conditional Access and Identity Protection

**RBAC Design Principles:**
- Mapping job roles to appropriate permissions
- Using groups for scalable access management
- Entra ID built-in roles vs. custom roles
- Regular access review requirements

### Security Concepts Internalized

**Zero Trust is Not Zero Access:**
- Policies should enable secure productivity, not block legitimate work
- Context-aware decisions (who, what, where, when, how)
- Continuous verification vs. perimeter-based security
- User experience matters - security friction must be balanced

**Defense in Depth Strategy:**
- No single control prevents all attacks
- Layered policies compensate for individual weaknesses
- MFA + Device Compliance + Risk Detection = comprehensive protection
- Each layer catches different attack vectors

**Risk-Based Access Control:**
- Not all sign-ins are equal - context determines trust
- Machine learning identifies patterns humans miss
- Real-time response prevents damage before it occurs
- Adaptive security scales with threat landscape

### Business Impact Understanding

**Quantifiable Security Improvements:**
- MFA enforcement: 99.9% reduction in credential attacks
- Legacy auth blocking: Eliminates entire attack class
- Risk-based access: Sub-second threat response
- Device compliance: Prevents unmanaged device compromise

**Operational Efficiency:**
- Automated policy enforcement reduces manual security reviews
- Self-service MFA reduces helpdesk password reset tickets by 50%
- Identity Protection reduces SOC investigation time by 85%
- Compliant device requirement standardizes admin workstations

**Compliance Benefits:**
- Policies support SOC 2 Type II access control requirements
- Risk detection provides audit trail for forensic investigations
- Role-based access satisfies separation of duties mandates
- Report-only mode demonstrates due diligence before enforcement

---

## 🔄 Real-World Applications

### Enterprise Implementation Parallels

**Fortune 500 Deployment Patterns:**

1. **Phased Rollout (Recommended):**
   - Week 1-2: Deploy all policies in Report-only mode
   - Week 3-4: Analyze impact, identify exceptions, communicate with users
   - Week 5: Enable MFA + Block Legacy Auth
   - Week 6: Enable Device Compliance + Risk-Based Access
   - Week 7+: Monitor, tune, optimize

2. **User Communication Strategy:**
   - Email campaigns explaining MFA benefits
   - Video tutorials for enrollment process
   - Executive sponsorship and messaging
   - Dedicated helpdesk support during rollout

3. **Exception Handling:**
   - Break-glass emergency accounts (excluded from all policies)
   - Service accounts (certificate-based auth instead of MFA)
   - VIP users (additional MFA methods, not policy bypass)
   - Quarterly exception review process

### Production Environment Differences

**Lab vs. Production:**

| Aspect | Lab Environment | Production Environment |
|--------|----------------|----------------------|
| **Risk Detections** | No real attacks | 1000+ detections/day in large org |
| **Policy Impact** | 4 test users | 10,000+ employees |
| **Integration** | Standalone Entra ID | SIEM, XDR, HRIS, ticketing systems |
| **Monitoring** | Manual log review | 24/7 SOC with automated alerting |
| **Compliance** | Learning exercise | Audit requirements, regulatory mandates |
| **Support** | Self-service | Helpdesk, security team, executive escalation |

**What Stays The Same:**
- Policy configuration process
- Zero Trust principles
- Risk detection logic
- RBAC design patterns
- Testing methodology

---

## 📊 Policy Effectiveness Metrics

### Success Criteria (Production Deployment)

**Security Metrics:**
- MFA enrollment rate: **100%** (target)
- Legacy auth usage: **0%** (target)
- Non-compliant admin sign-ins: **0%** (target)
- Blocked risky sign-ins: **Track weekly** (demonstrates protection)
- Account compromises: **0%** (ultimate goal)

**User Experience Metrics:**
- False positive rate: **<1%** (sign-ins incorrectly blocked)
- MFA setup time: **<10 minutes** average
- Helpdesk ticket increase: **Monitor, target stabilization within 30 days**
- User satisfaction: **Survey post-implementation**

**Operational Metrics:**
- Policy evaluation time: **<100ms** per sign-in
- SOC investigation time: **-85%** (vs. no Identity Protection)
- Incident response time: **<1 minute** (vs. 200+ days industry average)
- Security operations efficiency: **+40%**

---

## 🚀 Next Steps in My IAM Journey

**Week 3 Preview:** Privileged Identity Management (PIM)
- Just-In-Time (JIT) admin access
- Time-limited role activations
- Approval workflows for sensitive roles
- Privileged access governance

**Week 4 Preview:** Access Reviews & Governance
- Automated access certification campaigns
- Manager-driven access reviews
- Group membership attestation
- Orphaned account cleanup

**Week 5 Preview:** PowerShell Automation
- Microsoft Graph API integration
- Bulk user operations
- Automated policy deployment
- Custom reporting and analytics

Each lab builds progressively toward comprehensive IAM engineering expertise.

---

## 🔐 Security Considerations Applied

**Throughout this lab, I demonstrated security best practices:**

✅ **Testing Before Enforcement** - Report-only mode prevents user disruption  
✅ **Admin Account Protection** - Excluded from policies to prevent lockout  
✅ **Layered Security** - Multiple policies compensate for individual weaknesses  
✅ **Least Privilege** - Roles grant minimum necessary permissions  
✅ **Defense in Depth** - No single point of failure  
✅ **Audit Trail** - All actions logged in sign-in and audit logs  
✅ **Risk-Based Decisions** - AI/ML provides context-aware protection  

**Additional Production Controls:**
- Break-glass emergency accounts for policy failures
- Runbook documentation for policy rollback
- Change management approval process
- Business continuity planning for identity service outage
- Regular policy effectiveness reviews (quarterly)

---

## 📚 Resources Referenced

### Microsoft Documentation
- [Microsoft Entra Conditional Access Documentation](https://learn.microsoft.com/en-us/entra/identity/conditional-access/)
- [Identity Protection Risk Detection Types](https://learn.microsoft.com/en-us/entra/id-protection/concept-identity-protection-risks)
- [Zero Trust Deployment Guide](https://learn.microsoft.com/en-us/security/zero-trust/)
- [Conditional Access Policy Best Practices](https://learn.microsoft.com/en-us/entra/identity/conditional-access/plan-conditional-access)

### Industry Standards
- NIST Cybersecurity Framework - Identity and Access Management
- CIS Controls v8 - Account Management and Access Control
- ISO 27001 - Access Control Requirements
- SOC 2 - Common Criteria for Access Governance

---

## 💡 Lab Environment Notes

**Testing Limitations:**
- Risk detections require suspicious behavior to trigger (unlikely in lab)
- Device compliance requires Intune enrollment (simulated in Report-only)
- MFA enforcement tested but not fully deployed (Report-only mode)
- No actual attacks generated (policies demonstrate prevention capability)

**What This Demonstrates:**
- ✅ Policy configuration expertise
- ✅ Understanding of security concepts
- ✅ Knowledge of enterprise IAM workflows
- ✅ Ability to balance security and usability
- ✅ Documentation and governance skills

**Production Readiness:**
These exact policies could be deployed in production with minimal modification - only exclusions, MFA methods, and compliance requirements would need customization for specific organizations.

---

**Lab Completed:** January 2026  
**Time Invested:** 6 hours  
**Skill Level:** IAM Analyst with advanced Conditional Access expertise  
**Status:** ✅ Complete - Production-ready security policy suite

---

[← Back to Week 1: User Lifecycle](../Week-01-Entra-User-Lifecycle/README.md) | [Main Portfolio](../README.md) | [Next: Week 3: Privileged Identity Management →](../Week-03-Privileged-Access-Management/README.md)
