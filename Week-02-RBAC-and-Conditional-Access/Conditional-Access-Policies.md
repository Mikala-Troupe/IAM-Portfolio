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
