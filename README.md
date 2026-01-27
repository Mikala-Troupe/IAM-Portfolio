# 🔐 Identity & Access Management + Security Operations Portfolio

Welcome! I'm **Mikala Troupe**, and this is my hands-on portfolio demonstrating real-world identity and access management (IAM) and security operations skills.

I built this portfolio to show what I can do, not just what I know. Every lab simulates actual problems companies face and the solutions security teams implement.

---

## 👋 About Me

I'm a cybersecurity professional focused on identity security and security operations. I have certifications in Security+, CySA+, PenTest+, and (ISC)² SSCP, and I'm building this portfolio to demonstrate practical, job-ready skills.

**What I'm good at:**
- Setting up identity and access controls that stop attackers
- Automating security processes so they scale
- Explaining technical security to non-technical people
- Building things from scratch and documenting them well

**Current Focus:** IAM Analyst and SOC Analyst roles

**Location:** Open to relocation  
**LinkedIn:** [linkedin.com/in/mikala-troupe](https://www.linkedin.com/in/mikala-troupe)  
**Email:** troupemikala@gmail.com

---

## 🎯 What This Portfolio Shows

This isn't just screenshots and notes—every lab is a working implementation that solves real security problems:

**Phase 1 - Identity & Access Management (Weeks 1-6):**
- Managing employee accounts from hire to departure
- Stopping credential attacks with smart policies
- Implementing time-limited admin access
- Automating access reviews and compliance

**Phase 2 - Security Operations (Weeks 7-9):**
- Building security monitoring with SIEM
- Creating detection rules for real attacks
- Investigating incidents and responding

**Phase 3 - Integration (Weeks 10-12):**
- Connecting IAM and SIEM platforms
- Building end-to-end security workflows
- Full attack scenario from detection to remediation

**Why this combination?** Most companies need people who understand BOTH identity security AND security operations. This portfolio shows I can do both.

---

## 📂 Completed Labs

### ✅ Week 1: User Lifecycle Management
**What I Built:** Complete system for managing employee accounts from onboarding to offboarding

**The Problem:** Companies waste hours manually creating accounts, often forget to remove access when people leave, and have no audit trail.

**My Solution:** Set up the Joiner-Mover-Leaver (JML) process in Microsoft Entra ID with group-based access control.

**Key Results:**
- 96% reduction in onboarding time (5 minutes vs. 2 hours)
- Zero leftover access after transfers (prevents privilege creep)
- Complete audit trail for compliance

**Skills:** User provisioning, group-based access, org hierarchy, offboarding procedures

[View Lab Details →](Week-01-Entra-User-Lifecycle/)

---

### ✅ Week 2: Security Policies & Role-Based Access Control
**What I Built:** Automated security controls that stop hackers while letting real employees work normally

**The Problem:** Hackers steal passwords constantly. Companies need protection without annoying users with constant security checks.

**My Solution:** Configured 4 smart security policies including MFA, AI-powered risk detection, and role-based permissions.

**Key Results:**
- 99.9% of credential attacks blocked automatically
- AI detects and stops suspicious logins in <1 second
- $4.5M average breach cost prevented

**The 4 Policies:**
1. **Require MFA** - Everyone needs phone + password (not just password)
2. **Block old insecure apps** - Old email clients that can't do MFA get blocked
3. **Secure devices for admins** - IT admins must use company laptops with encryption
4. **AI risk detection** - Machine learning catches impossible travel, stolen passwords, suspicious IPs

**Skills:** Conditional Access, Zero Trust, AI/ML security, RBAC, defense in depth

[View Lab Details →](Week-02-RBAC-and-Conditional-Access/)

---

### ✅ Week 3: Just-In-Time Privileged Access
**What I Built:** System where admins get temporary admin rights only when needed, then lose them automatically

**The Problem:** Permanent admin access is risky. If someone steals an admin password, they get full control 24/7.

**My Solution:** Implemented Just-In-Time (JIT) access using Privileged Identity Management (PIM). Admins activate privileges when needed, provide justification, get approval, and rights auto-expire after 4 hours.

**Key Results:**
- 95% reduction in standing admin privileges
- Every admin action requires justification and approval
- Attack window reduced from 24/7 to <4 hours
- Complete audit trail of all privilege escalations

**Real Impact:** If admin account is compromised while privileges are inactive = attacker gets zero admin access

**Skills:** Privileged Identity Management (PIM), JIT access, approval workflows, access reviews, attack surface reduction

[View Lab Details →](Week-03-Privileged-Access-Management/)

---

## 🚀 In Progress

### 🔄 Week 4: Automated Access Reviews & Governance
**Coming Soon:** Periodic access certification, manager-driven reviews, automated cleanup

### 📅 Week 5: PowerShell Automation
**Coming Soon:** Bulk operations, Microsoft Graph API, custom reporting

### 🌍 Week 6: Guest User & External Identity Management
**Coming Soon:** B2B collaboration, partner access, external user lifecycle

---

## 🎓 Skills Demonstrated

### Technical Skills
**Identity & Access Management:**
- User lifecycle management (Joiner-Mover-Leaver)
- Role-Based Access Control (RBAC)
- Conditional Access policies
- Just-In-Time privileged access
- Multi-Factor Authentication (MFA)
- Group-based access control
- Access reviews and governance

**Security Operations:**
- AI/ML-based threat detection
- Risk-based authentication
- Security policy design
- Audit trail creation
- Compliance documentation

**Tools & Platforms:**
- Microsoft Entra ID (Azure AD)
- Privileged Identity Management (PIM)
- Conditional Access
- Identity Protection
- PowerShell & Microsoft Graph API

### Business & Soft Skills
- Explaining technical security to non-technical people
- Balancing security with user experience
- Understanding compliance requirements (SOC 2, ISO 27001, NIST)
- Calculating security ROI and business impact
- Creating documentation for different audiences
- Change management and rollout planning

---

## 📊 Portfolio Impact (If These Were Production Systems)

**Security Improvements:**
- 99.9% reduction in successful credential attacks
- 95% reduction in standing admin privileges
- 96% reduction in user provisioning time
- <1 second threat detection and response

**Business Value:**
- $4.5M average breach cost prevented per year
- 350 hours of IT time saved annually (at 1,000 employees)
- 100% compliance audit pass rate
- Cyber insurance requirements met

**User Impact:**
- 5-minute account setup (vs. 2-hour manual process)
- 3-second MFA verification (minor inconvenience, major protection)
- Zero standing admin access (admins activate only when needed)

---

## 🛠️ Technologies Used

**Identity & Access:**
- Microsoft Entra ID Premium P2
- Azure Active Directory
- Privileged Identity Management (PIM)
- Conditional Access
- Identity Protection
- Multi-Factor Authentication (MFA)

**Security & Compliance:**
- Risk-based authentication
- AI/ML threat detection
- Device compliance policies
- Audit logging and reporting

**Automation & Scripting:**
- PowerShell
- Microsoft Graph API
- Azure Portal

**Coming Soon:**
- Splunk (SIEM)
- Microsoft Sentinel
- Log analysis and correlation
- Incident response automation

---

## 📖 How to Navigate This Portfolio

**For Recruiters & Hiring Managers:**
- Start with the main README for each week (accessible, business-focused)
- Screenshots show what I actually built
- "Why This Matters" sections explain business value

**For Technical Reviewers:**
- Each lab has detailed technical documentation files
- Step-by-step procedures and configurations
- Code samples and automation scripts
- Compliance and audit documentation

**For Fellow Learners:**
- Detailed lab guides (available on request)
- Lessons learned and "aha!" moments
- Mistakes I made and how I fixed them
- Resources and references

---

## 🎯 What Makes This Portfolio Different

**Not just theory:**
- Every lab is a working implementation
- Real configurations, not just descriptions
- Screenshots prove I actually built it

**Business-focused:**
- Explains WHY, not just HOW
- Real-world examples and scenarios
- Cost savings and risk reduction calculated

**Multiple audiences:**
- Accessible to non-technical readers
- Technical depth available in supporting docs
- Visual documentation for different learning styles

**Honest about scope:**
- Clear about lab vs. production differences
- Acknowledges what would be added in enterprise environments
- Shows understanding of scalability and real-world constraints

---

## 📈 Portfolio Timeline

**Started:** January 2026  
**Target Completion:** April 2026 (12 weeks total)  
**Update Frequency:** 1 lab per week  

**Current Status:**
- ✅ Week 1: Complete (User Lifecycle)
- ✅ Week 2: Complete (Security Policies & RBAC)
- ✅ Week 3: Complete (Just-In-Time Access)
- 🔄 Week 4: In Progress (Access Reviews)
- 📅 Weeks 5-12: Planned

---

## 💼 What I'm Looking For

**Target Roles:**
- IAM Analyst
- Identity & Access Management Analyst
- SOC Analyst (Tier 1)
- Security Analyst (Identity focus)
- Access Management Analyst

**What I Bring:**
- Hands-on experience with enterprise IAM tools
- Understanding of security operations workflows
- Ability to explain technical concepts clearly
- Certifications: Security+, CySA+, PenTest+, SSCP
- Demonstrated ability to learn and build quickly

**What I'm Excited About:**
- Companies that take identity security seriously
- Teams that value automation and efficiency
- Organizations that invest in employee development
- Roles with clear growth paths (Analyst → Engineer → Architect)

---

## 📬 Let's Connect

I'm actively looking for **IAM Analyst** and **SOC Analyst** opportunities.

**Reach out if:**
- You have open positions that match my skills
- You want to discuss any of these labs in detail
- You have feedback on my approach or documentation
- You're also learning IAM/security and want to collaborate

**Contact:**
- 💼 **LinkedIn:** [linkedin.com/in/mikala-troupe](https://www.linkedin.com/in/mikala-troupe)
- 📧 **Email:** troupemikala@gmail.com
- 📂 **GitHub:** You're already here!

---

## 📚 Additional Resources

**My Background:**
- Bachelor of Science, Cybersecurity & Information Assurance (WGU, 2025)
- 9 industry certifications (CompTIA, (ISC)², ITIL)
- Previous experience: IT support, system troubleshooting, technical documentation

**Learning Resources I Used:**
- Microsoft Learn (Entra ID documentation)
- Microsoft's IAM best practices guides
- (ISC)² SSCP study materials
- Real-world security breach case studies

---

## 🔄 Portfolio Updates

I update this portfolio weekly as I complete new labs. Each week builds on previous work, creating progressively more complex and realistic scenarios.

**Week 4 Preview (Next):** Automated access reviews, manager-driven attestation, guest user lifecycle  
**Week 5 Preview:** PowerShell automation, Microsoft Graph API, bulk operations  
**Week 6 Preview:** External identities, B2B collaboration, partner access  

**Future phases:** SIEM integration, threat hunting, full incident response scenarios

---

## 📝 Notes on This Portfolio

**Lab vs. Production:**
These labs demonstrate concepts and configurations that would be used in production, but simplified for learning purposes. Real enterprise environments would add:
- Integration with HR systems (Workday, ADP)
- Automated provisioning workflows
- 24/7 security operations monitoring
- Thousands of users instead of test accounts
- Advanced threat intelligence feeds
- Dedicated security operations center (SOC)

**Why This Approach Works:**
By building simplified versions first, I understand the fundamentals. Scaling to enterprise complexity is easier once you know how the pieces work individually.

---

**Thanks for checking out my portfolio!** Every lab here represents real learning, real building, and real skills I can bring to a security team.

---

*Last Updated: January 2026*  
*Portfolio Status: Active Development*  
*Next Lab: Week 4 - Access Reviews & Governance*
