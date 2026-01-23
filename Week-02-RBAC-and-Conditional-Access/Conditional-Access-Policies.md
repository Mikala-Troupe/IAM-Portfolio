# Conditional Access Policies

## Policy Summary

| Policy Name | Target Users | Conditions | Action | Status |
|------------|--------------|------------|--------|--------|
| Require MFA for All Users | All users | None | Require MFA | Report-only |
| Block Legacy Authentication | All users | Legacy auth clients | Block access | Report-only |
| Require Compliant Device for IT Admins | IT-Admins group | None | Require compliant device | Report-only |
| Block Risky Sign-in Attempts | All users | Sign-in risk (High/Medium) | Block access | Report-only |

---

## Policy 1: Require MFA for All Users

### Purpose
Enforce multifactor authentication to prevent credential-based attacks and strengthen authentication security across the organization.

### Configuration
- **Applies to:** All users
- **Target:** All cloud apps
- **Control:** Require multifactor authentication
- **Status:** Report-only (testing phase)

### Business Justification
- Reduces risk of account compromise by 99.9%
- Industry best practice for identity security
- Required for compliance frameworks (SOC 2, ISO 27001, NIST)
- Protects against password spray and credential stuffing attacks

### User Impact
- **First-time setup:** 5-10 minutes to configure MFA method
- **Daily usage:** Additional 3-5 seconds per sign-in
- **Methods supported:** Authenticator app, SMS, phone call, hardware token

### Implementation Considerations
- Exclude break-glass emergency accounts
- Provide user training and documentation
- Establish helpdesk procedures for MFA issues
- Monitor adoption rates during rollout

---

## Policy 2: Block Legacy Authentication

### Purpose
Prevent attacks using outdated authentication protocols that don't support modern security features like MFA.

### Configuration
- **Applies to:** All users
- **Conditions:** Exchange ActiveSync clients, Other clients (legacy protocols)
- **Control:** Block access
- **Status:** Report-only

### Business Justification
- Legacy protocols (IMAP, POP3, SMTP AUTH) don't support MFA
- Common attack vector for credential stuffing
- Microsoft recommendation for all tenants
- Required for Zero Trust architecture

### Blocked Protocols
- Basic authentication (username/password only)
- Exchange ActiveSync (older versions)
- IMAP/POP3
- Authenticated SMTP
- Legacy Office clients (Office 2013 and older)

### Migration Plan
1. **Week 1-2:** Identify users with legacy clients (Report-only mode)
2. **Week 3-4:** Notify affected users, provide modern alternatives
3. **Week 5:** Enable policy (Block mode)
4. **Ongoing:** Monitor for exceptions, provide support

---

## Policy 3: Require Compliant Device for IT Admins

### Purpose
Ensure administrative access only occurs from managed, secure devices that meet organizational security standards.

### Configuration
- **Applies to:** IT-Admins group (Tony Stark)
- **Target:** All cloud apps
- **Control:** Require device compliance
- **Status:** Report-only

### Business Justification
- Admins have elevated privileges requiring additional security
- Prevents admin access from personal/unmanaged devices
- Supports Zero Trust "never trust, always verify" principle
- Reduces insider threat risk

### Device Compliance Requirements
To be marked as compliant, devices must:
- ✅ Be enrolled in Microsoft Intune
- ✅ Have up-to-date operating system
- ✅ Have antivirus enabled and current
- ✅ Have disk encryption enabled (BitLocker/FileVault)
- ✅ Not be jailbroken/rooted
- ✅ Pass security baseline checks

### Admin Experience
- **Compliant device:** Seamless sign-in
- **Non-compliant device:** Access blocked with instructions to enroll/remediate
- **Personal devices:** Must be enrolled or use dedicated admin workstation

---

## Policy 4: Block Risky Sign-in Attempts

### Purpose
Leverage machine learning-based risk detection to block suspicious authentication attempts in real-time, preventing account takeovers before they occur.

### Configuration
- **Applies to:** All users
- **Conditions:** Sign-in risk level = High or Medium
- **Control:** Block access
- **Status:** Report-only (testing phase)

### How It Works

**Real-Time Risk Analysis:**
Microsoft Entra ID Protection analyzes 20+ signals during each sign-in attempt:
- Geographic location and velocity (impossible travel)
- Device fingerprinting and properties
- IP address reputation and threat intelligence
- Credential leak databases (HaveIBeenPwned, etc.)
- Behavioral patterns and historical activity
- Anonymous proxies, VPNs, Tor networks

Machine learning models calculate a risk score: **Low, Medium, or High**

### Risk Level Definitions

| Risk Level | What It Detects | Example Scenarios | Action |
|------------|-----------------|-------------------|--------|
| **High** | Very suspicious, likely malicious | Anonymous proxy/VPN, impossible travel, leaked credentials found in breach database, password spray attack from botnet | **BLOCK** |
| **Medium** | Moderately suspicious, unusual | Unfamiliar device/location, atypical travel pattern, suspicious IP, mass file downloads | **BLOCK** |
| **Low** | Slightly unusual but likely legitimate | Minor behavioral deviations, new but reasonable location | **ALLOW** (with MFA) |

### Detection Examples

#### Example 1: Credential Stuffing Attack
```
User: Peter Parker
Detection: Password spray + Leaked credentials
Risk: HIGH
Action: Blocked

Details: 
- Credential found in public breach database
- Attempted from botnet IP address (known threat actor infrastructure)
- Same password tried across 50+ accounts in 2 minutes

Result: 
- Account secured, access denied
- User notified to change password immediately
- Security team alerted for investigation
```

#### Example 2: Impossible Travel
```
User: Natasha Romanoff
Detection: Atypical travel
Risk: HIGH
Action: Blocked

Details:
- Signed in from New York at 9:00 AM EST
- Sign-in attempt from Moscow at 9:30 AM EST (30 minutes later)
- Physical travel time: 10+ hours (impossible)

Result:
- Access blocked automatically
- User contacted for verification
- Confirmed user was in NY, Moscow attempt was attack
- Credentials reset as precaution
```

#### Example 3: Anonymous Proxy
```
User: Tony Stark
Detection: Anonymous IP address
Risk: MEDIUM
Action: Blocked

Details:
- Sign-in attempted via Tor network
- IP associated with anonymization service
- Unusual for this user (always signs in from corporate network)

Result:
- Access blocked
- User contacted
- Confirmed user did not attempt sign-in
- MFA re-verification required
```

### Business Justification
- **Blocks 99.9% of credential-based attacks**
- Real-time protection against account takeover
- Machine learning improves detection accuracy over time
- Reduces incident response from hours to seconds
- Required for cyber insurance in many industries
- Prevents data breaches before they occur

### User Impact
- **Legitimate users:** Minimal friction (normal sign-ins proceed)
- **Suspicious behavior:** Immediate block until verified
- **False positives:** Rare (<1%) due to ML accuracy
- **Remediation:** Self-service via MFA or contact IT

### Integration with Security Operations

**SOC Analyst Workflow:**
1. **Alert generated:** High-risk sign-in blocked
2. **Initial triage:** Review risk detection details
3. **User contact:** Verify whether attempt was legitimate
4. **Action taken:** 
   - Legitimate: Whitelist location/device
   - Attack: Reset credentials, investigate scope
5. **Documentation:** Update incident ticket, notify management if needed

**SIEM Integration:**
```
Risk Detection → Entra ID Protection → Azure Sentinel → Automated Response
```

- High-risk detection triggers automatic ticket creation
- User account flagged for review
- Manager notification sent
- Temporary additional scrutiny applied to account

### Monitoring & Reporting

**Daily Tasks:**
- Review risky sign-ins dashboard
- Investigate all High-risk blocks
- Confirm false positives
- Update risk policies based on patterns

**Weekly Reports:**
- Total sign-ins analyzed
- Risk detections by type
- Blocked sign-ins (prevented attacks)
- False positive rate
- User remediation metrics

**Monthly Review:**
- Policy effectiveness analysis
- Risk trend identification
- Training needs assessment
- Policy tuning recommendations

---

## Report-Only Mode Strategy

All policies are currently in **Report-only mode** for testing and impact assessment:

### Benefits
- ✅ Policies evaluate but don't enforce (safe testing)
- ✅ Sign-in logs show what would have happened
- ✅ Identify false positives before production
- ✅ Measure user impact without disruption
- ✅ Build confidence in policy configuration

### Testing Timeline

| Week | Activity | Deliverable |
|------|----------|-------------|
| 1-2 | Report-only data collection | Sign-in log analysis |
| 3 | Impact assessment | Affected user list, false positive report |
| 4 | User communication | Training materials, FAQ, support procedures |
| 5 | Policy 1 & 2 enabled | MFA and Legacy Auth blocking |
| 6 | Policy 3 & 4 enabled | Compliant device and Risk-based blocking |
| 7+ | Monitoring & tuning | Ongoing optimization |

---

## Production Rollout Plan

### Phase 1: Enable MFA and Block Legacy Auth (Week 5)
**Policies:** 1, 2  
**Risk:** Low (high user acceptance, clear benefit)  
**Rollback plan:** Switch back to Report-only if issues arise

**Prerequisites:**
- User training materials published
- Helpdesk procedures documented
- MFA enrollment campaign launched
- Executive sponsorship communicated

**Success Criteria:**
- 95% MFA enrollment within 2 weeks
- <5% helpdesk ticket increase
- No critical business disruption

---

### Phase 2: Enable Compliant Device (Week 6)
**Policy:** 3  
**Risk:** Medium (requires device enrollment)  

**Prerequisites:**
- Intune enrollment process documented
- Admin devices enrolled and compliant
- Helpdesk trained on enrollment support
- Dedicated admin workstation program established

**Success Criteria:**
- 100% admin devices compliant
- Zero non-compliant admin sign-ins
- Clear remediation path for exceptions

---

### Phase 3: Enable Risk-Based Blocking (Week 6)
**Policy:** 4  
**Risk:** Low (ML-based, high accuracy)  
**Monitoring:** 24/7 SOC monitoring for first 72 hours

**Prerequisites:**
- SOC team briefed on risk detection types
- Incident response playbook created
- User communication prepared for potential blocks
- Executive stakeholder approval obtained

**Success Criteria:**
- <1% false positive rate
- All blocked sign-ins investigated within 4 hours
- Zero successful account compromises

---

## Success Metrics

### Security Metrics
- **MFA adoption rate:** Target 100%
- **Legacy auth usage:** Reduce to 0%
- **Non-compliant admin sign-ins:** 0%
- **Blocked risky sign-ins:** Track weekly (shows protection)
- **Account compromises:** Target 0 (prevented by CA policies)

### User Experience Metrics
- **False positive rate:** <1%
- **MFA setup time:** <10 minutes average
- **Help desk tickets:** Monitor increase, target stabilization
- **User satisfaction:** Survey post-implementation

### Compliance Metrics
- **Policy coverage:** 100% of users and apps
- **Exception requests:** Track and review quarterly
- **Audit findings:** 0 related to access control
- **Compliance framework alignment:** SOC 2, ISO 27001, NIST

---

## Exception Process

### When Exceptions Are Needed

**Process:**
1. **Submit request:** Via IT service portal with business justification
2. **Review:** Security team evaluates risk vs. business need
3. **Approval:** Requires CISO sign-off for admin-level exceptions
4. **Implementation:** Temporary exclusion (max 90 days) or permanent with compensating controls
5. **Review:** All exceptions reviewed quarterly

### Common Exceptions

**Break-glass emergency accounts:**
- Excluded from all policies
- Used only during identity service outage
- Access monitored and audited
- Credentials secured in physical safe

**Service accounts:**
- Certificate-based authentication instead of MFA
- Dedicated service principal accounts
- No interactive sign-in allowed
- Credentials rotated quarterly

**VIP users:**
- Additional MFA methods (hardware tokens)
- NOT excluded from policies
- Enhanced monitoring applied
- Executive awareness training provided

### Exception Documentation

Each exception must include:
- **Business justification:** Why is this needed?
- **Risk assessment:** What are the security implications?
- **Compensating controls:** What mitigates the risk?
- **Review date:** When will this be re-evaluated?
- **Approver:** Who authorized this exception?

---

## Incident Response Integration

### High-Risk Sign-in Blocked

**Automated Response (within 1 minute):**
1. Access blocked immediately
2. Alert sent to SOC team
3. Ticket created in ITSM system
4. User notification sent (if legitimate)

**SOC Analyst Actions (within 15 minutes):**
1. Review sign-in details and risk factors
2. Check user's recent activity history
3. Contact user via known phone number
4. Determine if legitimate or attack

**If Attack Confirmed:**
1. Keep account blocked
2. Force password reset
3. Revoke all active sessions
4. Enable enhanced monitoring (30 days)
5. Review account permissions
6. Check for data exfiltration
7. Brief management if high-profile user

**If False Positive:**
1. Document reason for false positive
2. Consider whitelisting location/device
3. Allow access after additional MFA verification
4. Update risk policy tuning backlog

---

## Monitoring and Continuous Improvement

### Daily Monitoring
- Review Sign-in logs for policy evaluation
- Check Identity Protection dashboard
- Investigate any blocked sign-ins
- Respond to user access issues

### Weekly Reports
- Policy effectiveness summary
- Risk detection statistics
- False positive analysis
- User adoption metrics
- Helpdesk ticket trends

### Monthly Reviews
- Policy tuning opportunities
- Exception request review
- Compliance validation
- Executive briefing preparation

### Quarterly Assessments
- Full policy audit
- Security posture evaluation
- Compliance framework alignment check
- Rollout plan adjustments
- Success metrics review against targets

---

## Policy Dependencies and Conflicts

### Policy Evaluation Order
1. MFA requirement (Policy 1) - Evaluated first
2. Legacy auth block (Policy 2) - Blocks before other checks
3. Risk-based blocking (Policy 4) - Can override MFA if risk too high
4. Device compliance (Policy 3) - Additional check for admins

### Conflict Resolution
- **Most restrictive policy wins**
- Block access takes precedence over grant access
- Multiple grant requirements: ALL must be satisfied
- Exception exclusions bypass all policies

---

## Compliance and Audit Support

### SOC 2 Type II Requirements
- ✅ CC6.1 - Logical access controls implemented
- ✅ CC6.2 - MFA required for all users
- ✅ CC6.6 - Access restricted to authorized devices
- ✅ CC7.2 - Risk-based authentication monitoring

### ISO 27001 Controls
- ✅ A.9.1.2 - Access to networks and services
- ✅ A.9.2.1 - User registration and de-registration
- ✅ A.9.4.2 - Secure log-on procedures
- ✅ A.12.4.1 - Event logging

### NIST Cybersecurity Framework
- ✅ PR.AC-1 - Identity and credential management
- ✅ PR.AC-7 - Authentication and authorization
- ✅ DE.CM-1 - Network monitoring for anomalies
- ✅ RS.AN-1 - Notifications from detection systems

### Audit Evidence
All policy configurations, decisions, and exceptions are:
- Logged in Entra ID audit logs (retained 90 days minimum)
- Exported monthly for long-term compliance storage
- Available for auditor review via secure portal
- Documented with business justification

---

## Training and Awareness

### User Training Materials

**MFA Enrollment Guide:**
- Step-by-step instructions with screenshots
- Video tutorial (5 minutes)
- FAQ covering common issues
- Helpdesk contact information

**Security Awareness:**
- Why MFA matters (prevent account takeover)
- How risk detection protects them
- What to do if blocked (contact IT)
- Best practices for secure sign-ins

### Helpdesk Training

**Topics Covered:**
- MFA enrollment support procedures
- Troubleshooting common MFA issues
- Device compliance remediation steps
- Risk detection false positive handling
- Escalation procedures for complex cases

**Knowledge Base Articles:**
- "How to enroll in MFA"
- "What if I lost my MFA device?"
- "Why was my sign-in blocked?"
- "How to make my device compliant"

---

## Future Enhancements

### Planned Improvements (Next 6 Months)

**Policy Enhancements:**
- Add Session Controls (limit session lifetime for admins)
- Implement App Protection Policies
- Add location-based access for sensitive apps
- Enable Continuous Access Evaluation (CAE)

**Automation:**
- Auto-remediation for low-risk detections
- Automated exception request workflows
- Self-service MFA reset portal
- Predictive risk modeling

**Integration:**
- Microsoft Defender XDR correlation
- SIEM enrichment with CA policy context
- SOAR playbook automation
- User behavior analytics (UEBA)

---

## Related Documentation

**See Also:**
- [RBAC-Matrix.md](RBAC-Matrix.md) - Role definitions and assignments
- [Risk-Detection-Scenarios.md](Risk-Detection-Scenarios.md) - Detailed threat scenarios
- Microsoft Entra ID Conditional Access Best Practices
- Zero Trust Deployment Guide for Microsoft 365

---

**Document Version:** 1.0  
**Last Updated:** January 2026  
**Document Owner:** IT Security Team  
**Next Review Date:** April 2026  
**Approval Status:** Approved by CISO  
**Classification:** Internal Use Only
