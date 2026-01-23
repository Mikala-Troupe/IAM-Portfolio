# Identity Protection - Risk Detection Scenarios

## Overview

This document provides detailed scenarios showing how Microsoft Entra ID Protection's machine learning-based risk detection works in production environments. While the lab environment doesn't generate real risk detections, this demonstrates understanding of how the technology operates at scale.

---

## How Identity Protection Works

### Real-Time Analysis Pipeline
```
User Sign-in Attempt
        ↓
Microsoft Entra ID Protection
        ↓
Analyze 20+ Signals:
  • IP reputation
  • Geographic location
  • Device fingerprint
  • Behavioral patterns
  • Credential leak databases
  • Threat intelligence
  • Anonymous proxies
        ↓
Machine Learning Risk Calculation
        ↓
Risk Score: Low / Medium / High
        ↓
Conditional Access Policy Evaluation
        ↓
Allow (with MFA) / Block / Require Additional Verification
```

### Signal Analysis

**Signals Evaluated Per Sign-in:**
- IP address reputation (threat intelligence feeds)
- Geographic location and travel velocity
- Device properties and fingerprinting
- Browser and application characteristics
- Time of day and access patterns
- Historical user behavior baseline
- Credential compromise databases
- Anonymous proxy/VPN detection
- Tor network identification
- Botnet IP addresses
- Malware-linked infrastructure
- Recent security events
- Failed authentication patterns
- Unusual resource access
- Application permission changes
- Session anomalies

---

## Risk Detection Types

### High-Risk Detections

#### 1. Anonymous IP Address
**Description:** Sign-in from anonymous proxy service, VPN, or Tor network

**Detection Signals:**
- IP address matches known anonymization services
- Exit node from Tor network
- Commercial VPN service
- Proxy service used to hide true location

**Real-World Example:**
```
User: peter.parker@company.com
Time: 2026-01-15 14:23 UTC
IP: 185.220.101.5 (Tor exit node)
Location: Germany
Device: Chrome on Windows 11
Risk: HIGH
Decision: BLOCKED

Investigation:
- Peter's normal pattern: Signs in from New York office
- Never used Tor before
- Contacted Peter: Confirmed he did NOT attempt this sign-in
- Likely credential compromise attempt

Action Taken:
- Access blocked automatically
- User credentials reset
- MFA re-enrollment required
- Security awareness training recommended
```

**Why This Matters:**
- Legitimate users rarely use anonymization services
- Common tactic for attackers hiding their location
- Often indicates stolen credentials being tested
- Tor usage violates most corporate acceptable use policies

---

#### 2. Atypical Travel (Impossible Travel)
**Description:** Sign-in from location physically impossible given time between attempts

**Detection Signals:**
- Geographic distance vs. time elapsed
- Travel speed would exceed commercial flight speed
- No connecting flights available in timeframe
- Physics-based impossibility calculation

**Real-World Example:**
```
Sign-in 1:
User: natasha.romanoff@company.com
Time: 2026-01-20 09:00 EST
Location: New York, USA
IP: 192.168.10.5 (Corporate network)
Device: Windows laptop
Result: SUCCESS

Sign-in 2:
User: natasha.romanoff@company.com
Time: 2026-01-20 09:45 EST (45 minutes later)
Location: Moscow, Russia
IP: 94.142.241.5
Device: Chrome on Android
Risk: HIGH
Decision: BLOCKED

Analysis:
- Distance: ~4,700 miles
- Time: 45 minutes
- Required speed: ~6,267 mph
- Fastest commercial flight: ~575 mph
- Conclusion: IMPOSSIBLE TRAVEL

Investigation:
- User confirmed she was in New York office entire day
- Moscow sign-in was attempted compromise
- Credential found in recent data breach

Action Taken:
- Moscow sign-in blocked
- Forced password reset
- Enhanced monitoring for 30 days
- Breach notification sent to affected users
```

**Why This Matters:**
- Clear indicator of credential compromise
- Attacker in different location than legitimate user
- One of the most reliable detection types
- Minimal false positives (except for VPN edge cases)

---

#### 3. Malware-Linked IP Address
**Description:** Sign-in from IP address associated with known malware or botnet activity

**Detection Signals:**
- IP appears in threat intelligence feeds
- Known command-and-control server
- Botnet participation detected
- Malware distribution source

**Real-World Example:**
```
User: tony.stark@company.com
Time: 2026-01-22 03:17 UTC
IP: 45.142.212.61
Location: Unknown
Device: Unknown
Risk: HIGH
Decision: BLOCKED

Threat Intelligence:
- IP flagged in Microsoft threat feed
- Associated with Emotet botnet
- 1,247 malware samples linked to this IP in last 30 days
- Known credential harvesting operations

Investigation:
- User contacted immediately
- Confirmed NOT Tony's sign-in attempt
- Tony's credentials found in dark web breach database
- Credentials used from 2018 (reused password)

Action Taken:
- Immediate account lockdown
- Forensic analysis of recent account activity
- All sessions terminated
- New credentials issued
- Company-wide password policy update
- Security awareness campaign launched
```

**Why This Matters:**
- Direct evidence of malicious infrastructure
- High confidence of attack
- Often part of larger campaign
- Indicates sophisticated threat actor

---

#### 4. Leaked Credentials
**Description:** User's credentials detected in public breach databases or dark web

**Detection Signals:**
- Credentials found in HaveIBeenPwned database
- Dark web monitoring alerts
- Credential stuffing attack patterns
- Password appears in breach compilations

**Real-World Example:**
```
User: pepper.potts@company.com
Time: 2026-01-18 22:10 UTC
IP: 103.253.145.12
Location: Philippines
Device: Chrome on Windows 10
Risk: HIGH
Decision: BLOCKED

Breach Detection:
- Email/password combination found in "Collection #1" breach
- Breach date: 2019
- Breach size: 773 million records
- Password: "Summer2019!" (reused from personal account)

Attack Pattern:
- 150 failed login attempts in 5 minutes
- Same password tried across multiple corporate accounts
- Credential stuffing attack automated via botnet

Investigation:
- Pepper's personal email was breached in 2019
- She reused the same password for work account
- Attacker obtained credentials and waited to use them

Action Taken:
- Account access blocked
- Forced password reset
- MFA enforcement
- Personal data breach notification
- Password manager training provided
- Company policy updated: No password reuse
```

**Why This Matters:**
- Proactive detection before successful compromise
- Addresses password reuse problem
- Microsoft monitors billions of breached credentials
- Prevents account takeover attempts

---

#### 5. Password Spray Attack
**Description:** Attacker tries common passwords against many accounts

**Detection Signals:**
- Same password tried across multiple accounts
- High velocity of attempts
- Distributed source IPs (botnet)
- Common password patterns

**Real-World Example:**
```
Attack Timeline: 2026-01-25 11:00-11:15 UTC

Attempts Detected: 847 accounts targeted
Password Tried: "Winter2026!"
Source IPs: 45 different IPs (botnet)
Success Rate: 0% (all blocked)
Risk: HIGH
Decision: ALL BLOCKED

Attack Pattern:
11:00 - Attempts start from 45 IPs simultaneously
11:03 - 200 accounts attempted
11:07 - 500 accounts attempted
11:12 - 847 accounts attempted
11:15 - Attack stops (detection triggered)

Detection:
- Microsoft identified password spray pattern
- All sign-in attempts flagged as HIGH risk
- Conditional Access blocked all attempts
- Zero successful compromises

Affected Accounts:
- peter.parker@company.com - BLOCKED
- natasha.romanoff@company.com - BLOCKED
- tony.stark@company.com - BLOCKED
- [844 more accounts] - ALL BLOCKED

Response:
- Global alert sent to security team
- All affected users notified
- Temporary additional MFA requirement added
- Source IPs added to threat intelligence
- Security awareness bulletin sent company-wide
```

**Why This Matters:**
- Coordinated attack against entire organization
- Tests weak password policies
- Without detection: 5-10% success rate typical
- Early detection prevents mass compromise

---

### Medium-Risk Detections

#### 6. Unfamiliar Sign-in Properties
**Description:** Sign-in from device, browser, or location not previously used

**Detection Signals:**
- New device fingerprint
- Different browser/OS combination
- Unusual for user's historical pattern
- First-time location

**Real-World Example:**
```
User: peter.parker@company.com
Baseline Pattern:
- Device: Windows 11 laptop (DESKTOP-PARKER)
- Browser: Chrome 120
- Location: New York office (192.168.10.0/24)
- Time: Monday-Friday, 8 AM - 6 PM EST

New Sign-in:
Time: 2026-01-19 23:45 EST (Saturday night)
Device: iPhone 15 Pro
Browser: Safari 17
Location: Brooklyn, NY (home address)
IP: 73.94.120.45 (Residential ISP)
Risk: MEDIUM
Decision: ALLOW with additional MFA verification

Analysis:
- First mobile device sign-in
- Outside normal work hours
- Residential IP (not corporate)
- BUT: Location reasonable (user's home)

User Experience:
1. Username/password accepted
2. Additional MFA challenge: "We noticed a new sign-in"
3. Authenticator app notification
4. User approves: "Yes, this is me"
5. Access granted
6. Device added to known devices

Result:
- Legitimate user access
- Additional security verification
- Device fingerprint learned for future
- No disruption to user
```

**Why This Matters:**
- Balances security with user experience
- Catches unusual access without false positives
- Adaptive authentication based on context
- Machine learning improves over time

---

#### 7. Atypical Sign-in Activity
**Description:** Unusual access patterns or behavior for specific user

**Detection Signals:**
- Different application access than normal
- Unusual time of day
- Access to resources not typically used
- Rapid succession of different locations

**Real-World Example:**
```
User: tony.stark@company.com
Normal Pattern:
- Accesses: Email, SharePoint, Teams
- Time: 7 AM - 7 PM EST weekdays
- Locations: Office, home
- Applications: 5-8 per day

Unusual Activity:
Time: 2026-01-21 03:30 AM EST (middle of night)
Applications Accessed:
- Azure Portal (admin)
- PowerShell console
- User management API
- Bulk data export tool
- 47 different apps in 30 minutes
Risk: MEDIUM
Decision: ALLOW but flagged for review

Investigation:
- SOC analyst contacted Tony next morning
- Tony confirmed: Emergency infrastructure maintenance
- Had approval from CTO
- Legitimate but unusual activity

Result:
- Activity was legitimate
- False positive correctly handled
- Pattern learned for future emergencies
- Procedure updated to notify SOC proactively
```

**Why This Matters:**
- Catches insider threats and compromised accounts
- Detects data exfiltration attempts
- Identifies unusual administrative activity
- Balances security monitoring with false positives

---

#### 8. Sign-in from Infected Device
**Description:** Sign-in from device with detected malware or security issues

**Detection Signals:**
- Antivirus detections
- Known malware signatures
- Device compliance failures
- Security baseline violations

**Real-World Example:**
```
User: tony.stark@company.com
Device: LAPTOP-STARK-01
Time: 2026-01-21 10:15 EST
Risk: MEDIUM
Decision: BLOCKED (non-compliant device)

Device Status:
- Windows Defender: 15 threats detected
- Last antivirus update: 45 days ago (policy: 7 days)
- BitLocker: Disabled (required: Enabled)
- OS version: Windows 10 21H2 (outdated)
- Firewall: Disabled

Compliance Check:
✗ Antivirus outdated
✗ Threats not remediated
✗ Disk encryption disabled
✗ OS patches missing
✗ Firewall disabled

User Experience:
1. Sign-in blocked
2. Message: "Your device doesn't meet security requirements"
3. Instructions provided:
   - Update Windows Defender
   - Remove detected threats
   - Enable BitLocker
   - Update to Windows 11
   - Enable firewall
4. Re-check compliance after remediation

Resolution:
- IT contacted automatically
- Remote assistance provided
- Device cleaned and updated
- Compliance verified
- Access restored
- User educated on device security
```

**Why This Matters:**
- Prevents compromised device access
- Enforces security hygiene
- Protects corporate data
- Reduces malware spread risk

---

#### 9. Mass Access to Sensitive Files
**Description:** Unusual volume of file downloads or data access

**Detection Signals:**
- High velocity file downloads
- Access to sensitive/classified data
- Unusual resource consumption
- Pattern inconsistent with job role

**Real-World Example:**
```
User: peter.parker@company.com
Normal Pattern:
- 5-10 file downloads per day
- Access to IT documentation
- Typical role: Helpdesk support

Unusual Activity:
Time: 2026-01-24 15:30-16:00 EST
Activity:
- 237 files downloaded in 30 minutes
- Mix of HR data, financial records, customer lists
- Files Peter never accessed before
- Total data: 4.2 GB
Risk: MEDIUM
Decision: FLAGGED for investigation

Investigation:
- SOC contacted Peter immediately
- Peter's computer had been left unlocked
- Coworker accessed files as a "prank"
- Coworker disciplined
- No data left premises

Action Taken:
- All downloaded files deleted
- Security awareness training (screen locking)
- Policy reminder: Never leave workstation unlocked
- Enhanced monitoring on both accounts (30 days)
```

**Why This Matters:**
- Detects potential data exfiltration
- Catches insider threats
- Identifies compromised accounts
- Prevents data breaches

---

## Lab Environment vs. Production

### Lab Environment (This Project)
- ✅ Policies configured correctly
- ✅ Interface and tools accessible
- ✅ Report-only mode tested
- ✅ Sign-in logs reviewed
- ❌ Real risk detections unlikely (no suspicious behavior generated)

**Why No Real Detections:**
- Test users signing in from same device/location consistently
- No credential leaks for test accounts
- No malicious infrastructure involved
- No attack patterns generated
- Lab is too predictable for ML to flag risk

---

### Production Environment

**Real-World Scale:**
- Analyzes millions of sign-ins daily
- Processes 65 trillion signals across Microsoft cloud
- Updates threat intelligence in real-time
- Learns from global attack patterns
- Continuous ML model improvement

**Detection Frequency (Large Organization):**
- 1,000+ risk detections per day
- 50-100 high-risk blocks per day
- 5-10 confirmed compromises prevented per week
- 1-2 false positives per day (<1%)

**Response Speed:**
- Risk analysis: <100 milliseconds
- Block decision: Immediate
- SOC notification: <1 minute
- Investigation start: <15 minutes
- User contact: <1 hour

---

## SOC Analyst Response Workflow

### 1. Alert Reception
```
HIGH RISK SIGN-IN DETECTED
User: peter.parker@company.com
Risk: HIGH - Anonymous IP + Leaked Credentials
Status: BLOCKED
Time: 2026-01-15 14:23 UTC
Location: Germany (Tor exit node)
Device: Unknown
```

### 2. Initial Triage (5 minutes)
**Actions:**
- Open sign-in details in Identity Protection dashboard
- Review all risk factors and signals
- Check user's recent activity history (last 7 days)
- Verify user's normal sign-in patterns
- Check if user is currently at work/online

**Red Flags:**
- Multiple risk factors (anonymous IP + leaked credentials)
- Location inconsistent with user's normal pattern
- Device never seen before
- Time unusual for this user

---

### 3. User Verification (10 minutes)
**Contact Process:**
- Call user's registered phone number (not email - could be compromised)
- Ask verification questions only user would know
- **Key Question:** "Did you attempt to sign in at 2:23 PM today?"

**If User Says NO:**
- Confirm account is already blocked (it is)
- Inform user their credentials may be compromised
- Schedule immediate credential reset
- Proceed to incident response

**If User Says YES:**
- Ask why they used Tor/anonymization service
- Review company acceptable use policy
- Determine if legitimate business need
- Consider exception or policy adjustment

---

### 4. Incident Response (If Attack Confirmed)

**Immediate Actions (0-15 minutes):**
1. ✅ Account already blocked by Conditional Access
2. Revoke all active sessions
3. Reset user credentials
4. Force MFA re-enrollment
5. Enable enhanced monitoring (30 days)

**Investigation (15-60 minutes):**
6. Review last 30 days of sign-in activity
7. Check for successful compromises before detection
8. Identify data accessed or exfiltrated
9. Review email rules (forwarding, delegation)
10. Check for privilege escalation attempts
11. Examine file downloads and uploads
12. Review application consent grants

**Containment (1-2 hours):**
13. Identify other affected accounts (same attack pattern)
14. Check for lateral movement to other users
15. Review shared resources accessed by account
16. Notify affected data owners
17. Preserve evidence for forensics

**Recovery (2-24 hours):**
18. User enrolls in MFA with new credentials
19. Restore access with enhanced monitoring
20. Review and restore legitimate email rules
21. Verify no persistent access mechanisms
22. Update security awareness for user

---

### 5. Documentation (15 minutes)
**Incident Ticket:** INC-2026-0115

**Required Information:**
- Incident timeline (detection → resolution)
- Risk factors identified
- User verification outcome
- Actions taken
- Data impact assessment
- Root cause analysis
- Lessons learned
- Recommendations

**Stakeholder Notifications:**
- Manager briefing (if sensitive data accessed)
- Executive report (if high-profile user)
- Legal/compliance (if regulatory data involved)
- Insurance carrier (if breach notification required)

---

### 6. Post-Incident Review (Within 7 days)

**Questions to Answer:**
- How did credentials get compromised?
- Was detection timely enough?
- Were response procedures followed correctly?
- Any improvements needed to detection?
- Any policy adjustments needed?
- User education required?

---

## Business Impact Analysis

### Attack Prevention Metrics

**Without Identity Protection + Conditional Access:**
```
Credential stuffing attack: 850 attempts
Without protection: ~42 accounts compromised (5% success rate typical)
Average breach cost per account: $4.45M / 1000 = $4,450
Total potential cost: 42 × $4,450 = $186,900

Plus:
- Data breach notification costs: $50,000
- Regulatory fines (GDPR, CCPA): $250,000+
- Reputation damage: Immeasurable
- Customer trust loss: Long-term revenue impact
- Incident response costs: $75,000
- Legal fees: $100,000+

Estimated Total Impact: $650,000+ per attack
```

**With Identity Protection + Conditional Access:**
```
Credential stuffing attack: 850 attempts
With protection: 0 accounts compromised (0% success rate)
Cost: $0

Prevention value: $650,000+ per attack
ROI: Infinite (no successful breaches)
```

---

### Real-World Impact (2023-2025 Industry Data)

**Organizations Using Conditional Access + Identity Protection:**
- 99.9% reduction in credential-based attacks
- 97% reduction in account takeover incidents
- 89% reduction in security incidents requiring investigation
- 85% reduction in incident response time
- Average time to detect compromise: <1 minute (vs. 200+ days industry average without)

**Cost Savings:**
- Average prevented breach cost: $4.45 million
- Security operations efficiency: +40%
- Incident response time: -85%
- Helpdesk password reset tickets: -50% (due to MFA)
- Insurance premium reduction: 15-30%
- Compliance audit costs: -25%

**Productivity Impact:**
- User sign-in time: +3 seconds (MFA)
- False positive lockouts: <1% of sign-ins
- MFA enrollment time: 10 minutes per user (one-time)
- Net productivity impact: Positive (prevents downtime from breaches)

---

## Integration with Security Stack

### SIEM Integration (Azure Sentinel)

**Event Flow:**
```
Entra ID Protection
        ↓
Risk Detection Event
        ↓
Azure Sentinel (SIEM)
        ↓
Correlation Rules:
  • Cross-check with firewall logs
  • Correlate with endpoint alerts
  • Check email security events
  • Review cloud app activity
        ↓
Automated Playbook:
  1. Create incident ticket (ServiceNow)
  2. Notify SOC analyst (Teams/Email)
  3. Block user account (automated)
  4. Trigger forensics collection
  5. Send executive notification (if high-profile)
  6. Create timeline dashboard
        ↓
Analyst Investigation
        ↓
Remediation & Closure
```

---

### XDR Integration (Microsoft Defender)

**Cross-Platform Correlation:**
```
Identity Risk (Entra ID)
        +
Endpoint Threat (Defender for Endpoint)
        +
Email Attack (Defender for Office 365)
        +
Cloud App Anomaly (Defender for Cloud Apps)
        =
Unified Incident View
```

**Example Correlated Incident:**
```
Timeline:
09:00 - Email phishing attempt delivered (Defender for Office 365)
09:05 - User clicks link, enters credentials (Defender for Cloud Apps)
09:06 - Credentials harvested by attacker
09:10 - Risky sign-in detected from Russia (Identity Protection)
09:10 - Malware installed on user's device (Defender for Endpoint)
09:11 - Lateral movement attempted (Defender for Identity)

Automated Response:
- All attacks blocked automatically
- User account isolated
- Device quarantined
- Incident created with full attack chain
- SOC notified with complete context
```

---

## Continuous Improvement

### Machine Learning Optimization

**Daily Model Updates:**
- Microsoft analyzes 65 trillion signals daily
- New threat patterns identified hourly
- Models retrain continuously
- False positive feedback loop improves accuracy
- Organization-specific baselines learned over time

**Signal Improvements:**
```
Month 1: 85% accuracy
Month 3: 92% accuracy
Month 6: 97% accuracy
Month 12: 99%+ accuracy (mature baseline)
```

---

### Threat Intelligence Updates

**Real-Time Intelligence Sources:**
- Microsoft Threat Intelligence Center
- Global sign-in telemetry
- Breach database monitoring (HaveIBeenPwned)
- Dark web credential monitoring
- Tor exit node databases
- VPN service IP ranges
- Botnet command & control infrastructure
- Malware distribution networks
- Zero-day threat indicators

**Update Frequency:**
- Threat intelligence: Real-time
- IP reputation: Every 15 minutes
- Credential breach data: Daily scans
- ML models: Continuous training
- Detection rules: Weekly tuning

---

## Advanced Scenarios

### Scenario: Compromised Service Account

**Detection:**
```
Service Account: svc-backup@company.com
Normal Pattern: Automated backups, 2 AM daily
Detection: Interactive sign-in at 2 PM from Brazil
Risk: HIGH
```

**Why High Risk:**
- Service accounts should never sign in interactively
- Location inconsistent with server location
- Time inconsistent with scheduled tasks
- Human behavior on non-human account

**Response:**
- Immediate account suspension
- Review recent API calls
- Check data accessed
- Rotate service account credentials
- Implement certificate-based auth instead

---

### Scenario: Account Takeover During Active Session

**Detection:**
```
User: natasha.romanoff@company.com
Session 1: New York (legitimate, ongoing)
Session 2: China (attacker, simultaneous)
Risk: CRITICAL
```

**Why Critical:**
- Two simultaneous sessions from impossible locations
- Indicates real-time compromise
- Attacker has valid session token
- Data exfiltration risk extremely high

**Response:**
- Terminate ALL sessions immediately
- Force re-authentication with MFA
- Lock account until user verified
- Review all activity in last 24 hours
- Notify user via phone immediately
- Escalate to incident response team

---

## Training Scenarios for SOC Analysts

### Exercise 1: Password Spray Response
**Scenario:** 500 accounts targeted in 10 minutes, same password

**Analyst Tasks:**
1. Identify attack pattern in logs
2. Verify all accounts were blocked
3. Check if any succeeded before detection
4. Extract source IPs and report to threat intel
5. Document attack timeline
6. Recommend security awareness training

---

### Exercise 2: False Positive Handling
**Scenario:** Executive traveling internationally, multiple blocks

**Analyst Tasks:**
1. Review executive's travel itinerary
2. Verify legitimate business travel
3. Provide temporary exception
4. Document business justification
5. Set expiration date for exception
6. Schedule post-travel review

---

### Exercise 3: Insider Threat Investigation
**Scenario:** Employee downloading customer database before resignation

**Analyst Tasks:**
1. Identify unusual data access pattern
2. Correlate with HR records (resignation filed)
3. Interview user with HR present
4. Preserve evidence for legal
5. Prevent data exfiltration
6. Report to legal/compliance team

---

## Conclusion

Identity Protection's risk-based detection represents a fundamental shift from **reactive security** (responding after breach) to **proactive prevention** (blocking attacks in real-time).

**Key Takeaways:**
- Machine learning provides context-aware security decisions
- 20+ signals analyzed per sign-in in <100ms
- 99.9% of credential attacks prevented
- Minimal user friction for legitimate access
- Continuous improvement through global telemetry

**Production Readiness:**
While this lab couldn't generate real risk detections, the configurations demonstrated are production-ready and reflect enterprise-grade security practices used by Fortune 500 companies.

---

**Document Version:** 1.0  
**Last Updated:** January 2026  
**Document Owner:** Security Operations Team  
**Review Frequency:** Quarterly  
**Next Review:** April 2026  
**Classification:** Internal Use - Training Material
