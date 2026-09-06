# Research Report: Social Engineering Attacks

## 1. Introduction

Social engineering is the use of deception, persuasion, and psychological pressure to make a person take an action that helps an attacker. Unlike a purely technical exploit, social engineering does not begin by attacking software code or a network port. It attacks the decision-making process of the user, employee, customer, or support staff member. The attacker may want a password, a multi-factor authentication code, a wire transfer, access to a device, or a small piece of information that can be combined with other details later.

Social engineering is effective because people naturally rely on trust and routine. Employees answer support calls, open business documents, help co-workers, respond to managers, and follow urgent instructions during normal work. Attackers abuse these normal habits. A phishing email may look like it came from a bank, delivery company, cloud service, or internal department. A pretexting attacker may act like an IT technician, vendor, government official, or new employee. A baiting attack may offer free software, a giveaway, or a found USB device that triggers curiosity.

The psychological techniques used in social engineering are simple but powerful. Trust makes a victim lower their guard. Fear can push someone to act quickly to avoid account closure, legal trouble, or job consequences. Urgency reduces careful review. Authority can make an instruction feel mandatory. Curiosity encourages people to open unknown files or devices. Greed and fear of missing out make fake rewards, discounts, and giveaways more convincing. Helpfulness can be exploited when employees want to solve a caller's problem without appearing difficult.

The 2024 Verizon Data Breach Investigations Report reported that 68% of breaches involved a non-malicious human element, such as a person making an error or falling victim to social engineering. Verizon also reported that in phishing simulation data, the median time for users to fall for phishing emails was less than 60 seconds. These numbers should not be read as blaming users. They show that attackers design social engineering to work fast, especially when people are busy, remote, distracted, or handling routine requests.

Social engineering is closely connected to cybersecurity incidents because it is often used for initial access. Once an attacker obtains a password, session token, remote access approval, or malware execution, the rest of the intrusion may look more technical. For this reason, employee awareness is a critical cybersecurity defense. A trained employee who stops, verifies, and reports a suspicious request can interrupt an attack before it becomes a breach.

## 2. Phishing

### 2.1 Definition and How Phishing Works

Phishing is a social engineering attack where the attacker sends a deceptive message that appears to come from a trusted person or organization. The message usually asks the victim to click a link, open an attachment, enter credentials, approve a login, call a phone number, or perform a financial action. Phishing commonly uses email, but it can also happen through text messages, social media, collaboration platforms, and voice calls.

Attackers create phishing messages by copying branding, login pages, language, and normal business workflows. A message may pretend to be from Microsoft 365, Google, a bank, a delivery service, an HR department, a payment platform, or an executive. The attacker may include a link to a fake login page that collects usernames and passwords. Some phishing sites also proxy the login session so the attacker can capture tokens or complete an adversary-in-the-middle attack. Other messages deliver malware through attachments, such as Office documents, archive files, PDFs, or fake installers.

Credential harvesting is one of the most common goals. If a victim enters credentials into a fake page, the attacker can use them against email, VPN, cloud storage, payroll systems, or other business applications. Malicious attachments work differently: the victim opens a file, enables content, or runs a disguised program, allowing malware to execute. Malware delivery may lead to remote access, ransomware, data theft, or further phishing from the victim's trusted account.

```text
Attacker prepares fake message
        |
        v
Victim receives trusted-looking email, text, or call
        |
        v
Victim opens link, attachment, or login page
        |
        v
Credentials, MFA approval, or malware execution occurs
        |
        v
Attacker gains access or steals information
```

MITRE ATT&CK tracks phishing under technique T1566 and includes sub-techniques such as spearphishing attachment, spearphishing link, spearphishing via service, and spearphishing voice. This shows that phishing is not a single email trick; it is a family of delivery methods used to gain access.

### 2.2 Types of Phishing

### Spear Phishing

Spear phishing is a targeted phishing attack against a specific person, team, company, or industry. The attacker researches the victim before sending the message. They may use LinkedIn, company websites, breached data, press releases, vendor lists, or social media to make the message believable. The primary targets are employees with useful access, such as finance staff, IT administrators, HR personnel, developers, and executives. The communication channel is usually email or a business messaging service. The technique is personalization: the message uses real names, job roles, projects, or business context. The potential impact is higher than ordinary phishing because the victim is more likely to believe the message is relevant.

### Whaling

Whaling is phishing that targets senior executives or other high-value leaders. Attackers may impersonate a CEO, CFO, board member, lawyer, or trusted business partner. The channel is usually email, but phone calls and messaging apps may also be used. Whaling is closely related to Business Email Compromise because the goal may be a wire transfer, payroll change, tax document request, or approval of a sensitive business action. The potential financial impact can be high because executives and finance leaders often have authority to approve large transactions.

### Vishing

Vishing is voice phishing. The attacker uses a phone call or voice message to manipulate the target. A common technique is fake technical support: the caller claims to be from IT, a bank, a government office, or a vendor and says there is an urgent problem. The target may be asked to reveal a code, install remote access software, reset a password, or approve MFA. Vishing uses urgency, fear, confidence, and authority. The impact can include account takeover, help desk compromise, payment fraud, or installation of remote access tools.

### Smishing

Smishing is SMS phishing. The attacker sends a text message that includes a malicious link or request. Common lures include fake delivery notifications, banking alerts, unpaid tolls, account locks, job offers, and prize notifications. The target is usually an individual user, but employees can also receive smishing messages on work phones. The channel is SMS or mobile messaging. The technique relies on short messages, urgency, and the fact that mobile screens make it harder to inspect links. The impact may include stolen credentials, malware installation, or fraud.

### 2.3 Real-World Case Study

### Background

A well-documented phishing and social engineering case is the July 2020 Twitter incident. The New York State Department of Financial Services published an investigation report on Twitter's July 15, 2020 cybersecurity incident. The organization targeted was Twitter, and the attack affected high-profile Twitter accounts belonging to public figures, companies, and cryptocurrency-related accounts.

### Attack Method

According to the NYDFS report, attackers called Twitter employees and pretended to be from Twitter's IT department. The attackers used the remote-work context and common VPN problems to make the calls believable. Employees were directed to a phishing website that looked like Twitter's real VPN login page. When some employees entered credentials into the fake site, the attackers attempted to use those credentials on the real system. In some cases, employees also approved MFA prompts, allowing the attackers to gain access.

The attack then moved beyond the first compromised employee. The attackers used internal access to learn about Twitter systems and targeted employees who had access to internal account tools. They eventually took control of multiple accounts and posted cryptocurrency scam messages from well-known profiles. Twitter's own public update also stated that attackers targeted employees through a social engineering scheme.

### Impact

NYDFS reported that 130 Twitter accounts were compromised, 45 accounts were used to send tweets, and account information was downloaded for seven accounts. The fraudulent tweets promoted a bitcoin scam and resulted in more than $118,000 worth of bitcoin being stolen. The impact was not only financial. The incident raised concerns about trust in a major communication platform because the compromised accounts included influential public figures and organizations.

### Lessons Learned

The attack succeeded because the callers used a believable work-related story, a fake login page, and real operational pressure during remote work. It also showed that MFA is important but can be bypassed if users approve prompts during a live phishing call. Stronger defenses include phishing-resistant MFA, tighter access controls for internal tools, help desk and employee verification procedures, privileged access monitoring, and regular reporting-focused awareness training.

### 2.4 Prevention Recommendations

### 1. Security Awareness Training

Employees should be trained to recognize suspicious senders, urgent language, unexpected attachments, mismatched links, unusual login pages, requests for credentials, and pressure to keep a request secret. Training should also explain how to report suspicious messages quickly. A reporting button or clear security mailbox helps employees act without wasting time.

### 2. Multi-Factor Authentication

Passwords alone are not enough because phishing is often designed to steal them. MFA adds another verification step and can reduce the chance that a stolen password immediately becomes account access. However, MFA does not completely eliminate phishing risk. Push fatigue, stolen session tokens, adversary-in-the-middle phishing, and social engineering against help desks can still defeat weak MFA implementations. CISA and NIST recommend stronger, phishing-resistant approaches such as FIDO/WebAuthn or certificate-based authentication where possible.

### 3. Email Security Controls

Email security controls reduce the number of malicious messages that reach users. Spam filtering blocks known unwanted or suspicious messages. Attachment scanning inspects files for malware, suspicious macros, scripts, and risky file types. URL filtering checks links before users reach malicious pages. SPF helps receiving mail servers verify whether a sending server is authorized for a domain. DKIM signs email so receivers can verify that the message has not been altered and came from a domain-controlled key. DMARC builds on SPF and DKIM by telling receivers how to handle messages that fail authentication, which helps reduce direct domain spoofing.

### 4. Verification Procedures

Employees should verify unusual requests through independent channels. For example, a payment request from an executive should be confirmed by calling a known company number or using an approved workflow, not by replying to the same email. Users should avoid clicking login links in unexpected messages and instead navigate to the official website or application directly. Verification is especially important for password resets, bank details, gift card requests, urgent file sharing, and requests involving sensitive data.

## 3. Pretexting

### 3.1 Definition

Pretexting is a social engineering technique where the attacker creates a believable false identity and story to persuade the victim to provide information or perform an action. The pretext is the fabricated situation designed to manipulate the target. It may be as simple as "I am from IT and need to verify your account" or as detailed as a fake vendor support case, legal request, HR process, customer complaint, or delivery issue.

Pretexting works because people respond to context. If the story fits the victim's job role and current environment, it may not feel suspicious. Attackers establish trust by using real names, business terms, employee details, ticket numbers, caller ID spoofing, or knowledge collected from public sources. Once trust is created, the attacker requests sensitive information, access approval, a password reset, a document, or a change to account settings.

### 3.2 How Pretexting Works

A typical pretexting attack follows a lifecycle:

1. Information gathering: The attacker collects details about the organization, employees, vendors, tools, and workflows.
2. Target research: The attacker selects a person who can provide useful access or information.
3. Creation of false identity: The attacker chooses a role such as employee, IT support, auditor, vendor, customer, or government representative.
4. Development of a believable scenario: The attacker builds a story that explains why the request is normal and time-sensitive.
5. Establishing trust: The attacker uses known details, polite confidence, authority, or urgency to make the victim comfortable.
6. Requesting sensitive information: The attacker asks for credentials, reset approval, personal data, payment changes, or internal documents.
7. Exploiting the information: The attacker uses the result for account access, fraud, reconnaissance, or a larger intrusion.

```text
Research target
      |
      v
Create believable identity and story
      |
      v
Contact victim through phone, email, chat, or in person
      |
      v
Build trust and pressure
      |
      v
Collect access, data, approval, or payment
```

### 3.3 Real-World Case Study

### Background

A documented example of pretexting and impersonation appears in reporting on UNC3944, also known in public reporting as Scattered Spider. Mandiant has described UNC3944 as a financially motivated threat group that relies heavily on SMS phishing, SIM swapping, and phone-based impersonation. CISA's Scattered Spider advisory also notes the group's use of social engineering techniques, including phishing, push bombing, and SIM swap attacks, to obtain credentials and bypass MFA.

### Attacker's Pretext

In documented UNC3944 activity, attackers impersonated legitimate employees when contacting service desks. The pretext often involved account access trouble, phone changes, MFA reset needs, or other normal support situations. These are believable scenarios because real employees frequently contact help desks for password and MFA problems.

### Attack Method

Mandiant reported that attackers used stolen or gathered information such as usernames, employee IDs, and other personal details to answer help desk verification questions. In some cases, attackers used smishing to obtain credentials first, then called service desks to reset MFA or obtain access. This combination of stolen data and confident impersonation made the caller appear legitimate.

### Impact

The impact of this style of attack can be severe because help desks often control identity recovery. If an attacker convinces support staff to reset MFA, enroll a new device, or issue temporary credentials, the attacker may gain access without exploiting a software vulnerability. From there, they can access cloud applications, internal documentation, remote access systems, and sensitive data. Public reporting and advisories link Scattered Spider-style intrusions to extortion and ransomware activity across targeted organizations.

### Lessons Learned

The main lesson is that help desk verification is a security control, not only a customer service process. Knowledge-based questions are weak when the answers can be found in employee records, breaches, or public profiles. Stronger controls include verified callbacks, manager approval for high-risk resets, phishing-resistant MFA enrollment processes, identity proofing, privileged access monitoring, and training support staff to slow down unusual requests.

### 3.4 Prevention Measures

### 1. Identity Verification

Organizations should verify employees, vendors, callers, and support requesters through official channels. A caller asking for a reset should be confirmed using a known directory number, approved ticketing process, device trust signal, manager approval, or identity proofing workflow. Verification should not depend only on information the caller provides.

### 2. Security Awareness Training

Employees should learn to recognize suspicious scenarios, not only suspicious emails. Training should include phone calls, chat messages, vendor impersonation, fake IT support, fake HR requests, and pressure tactics. Staff should be encouraged to question unusual requests politely and report them without fear.

### 3. Least Privilege and Information Protection

Least privilege limits what one manipulated person can expose. Employees should only have access to data and systems required for their role. Sensitive information such as employee IDs, reset procedures, internal diagrams, and customer data should not be shared unnecessarily. Role-based access controls, logging, and approval workflows make pretexting less damaging when it succeeds.

### 4. Strong Help Desk Procedures

Help desk teams should have written procedures for password resets, MFA resets, device enrollment, and privileged account recovery. High-risk requests should require stronger verification than routine questions. Repeated failed verification, refusal to use official channels, or urgent pressure should trigger escalation.

## 4. Baiting

### 4.1 Definition

Baiting is a social engineering attack where the attacker offers something attractive or interesting to make the victim take a risky action. The bait may be physical, such as a USB drive left in a parking lot or mailed as a gift. It may also be digital, such as fake free software, a cracked application, a fake giveaway, a malicious advertisement, or a fake security tool.

Baiting uses curiosity, greed, fear of missing out, and the desire for free resources. A victim may connect an unknown device because they want to return it to the owner, see what is on it, claim a reward, or use a free tool. The difference between physical and digital baiting is the delivery method. Physical baiting uses objects. Digital baiting uses online content, downloads, advertisements, or links.

### 4.2 Physical Baiting

Physical baiting often uses removable media or hardware. An attacker may leave infected USB drives in public areas near a target organization, mail devices to selected employees, or disguise a malicious device as a normal storage drive. Some devices act like keyboards rather than storage. When plugged in, they can automatically type commands, open a terminal, run PowerShell, or download malware.

```text
Attacker prepares malicious device
        |
        v
Device is left, mailed, or disguised as a gift
        |
        v
Victim connects it to a work computer
        |
        v
Malware runs or commands are injected
        |
        v
System access, credential theft, or network compromise
```

Consequences can include malware infection, ransomware deployment, credential theft, data exfiltration, and movement from one workstation into the wider network. Even if removable storage is blocked, a BadUSB-style device may succeed if the system trusts it as a keyboard.

### 4.3 Digital Baiting

Digital baiting uses online offers and downloads. Examples include fake free software, pirated applications, game cheats, fake browser updates, fake security tools, malicious advertisements, fake coupons, and giveaway pages. Victims may be redirected to malware, credential theft pages, or downloads that look useful but install unwanted programs.

The attack works because the victim believes they are receiving something valuable. A cracked software installer may include an infostealer. A fake antivirus tool may display warnings and request payment. A malicious advertisement may redirect users to a fake update page. Digital baiting is especially risky when users search for free versions of paid software or install tools from unofficial sources.

### 4.4 Real-World Case Study

### Background

A documented baiting case involved FIN7, a financially motivated cybercriminal group. Public reporting from Mandiant and security advisories described campaigns where malicious USB devices were mailed to organizations. The targets included businesses in sectors such as retail, restaurant, hotel, and other commercial environments.

### Bait Used

The bait was a physical package. Some reports described packages that included items such as gift cards, branded-looking letters, or other props that made the mailing appear legitimate. The USB device was presented as something the recipient had a reason to connect, such as a device related to a reward, product list, or business message.

### Attack Method

The malicious USBs were not ordinary flash drives. They used BadUSB-style behavior, meaning the device could act as a keyboard and inject commands after being connected. Mandiant reported that a 2021 campaign mailed BadUSB devices that downloaded additional malware and ultimately installed the DICELOADER framework. UCLA's security advisory, summarizing FBI-observed activity, described FIN7 devices that injected keystrokes to run PowerShell commands and download malware.

### Impact

The intended impact was unauthorized access to target systems. Once malware was installed, attackers could conduct reconnaissance, move laterally, steal data, or support later ransomware and extortion activity. This case is important because it shows that baiting can bypass email filters entirely. The attack arrives through physical mail and depends on the user's decision to trust an unexpected object.

### Lessons Learned

Unknown devices should be treated as security risks even when they arrive in professional-looking packaging. Organizations need technical controls such as USB restrictions and endpoint detection, but they also need training for employees who receive mail, gifts, or vendor materials. A suspicious package should be reported to security instead of tested on a work computer.

### 4.5 Prevention Measures

### 1. Restrict Unauthorized USB Devices

Organizations should use USB device control policies to block unknown removable media and unauthorized Human Interface Device behavior where possible. Endpoint security tools can enforce allowlists, monitor suspicious PowerShell activity, and prevent automatic execution. Device policies should be tested because some BadUSB devices do not behave like normal storage.

### 2. Download Software Only from Trusted Sources

Employees should install software only from official websites, approved vendor portals, managed app stores, or verified internal repositories. Software signatures and hashes should be checked for important tools. Pirated software, unofficial installers, and fake updates should be blocked because they are common bait for malware.

### 3. Security Awareness Training

Training should explain the risks of unknown USB devices, fake downloads, free software offers, and promotional packages. Employees should know how to report suspicious devices and should never plug an unknown device into a work system to investigate it.

### 4. Endpoint Detection and Application Allowlisting

Endpoint detection and response can identify suspicious behavior such as unexpected script execution, credential dumping, command-and-control traffic, or unusual process chains. Application allowlisting reduces the chance that unauthorized programs, scripts, or installers will run even if a user is tricked.

## 5. Quid Pro Quo Attacks

Quid pro quo means "something for something." In social engineering, a quid pro quo attack occurs when an attacker offers help, a service, a benefit, or a reward in exchange for information or access. A common scenario is fake technical support. The attacker offers to fix a computer issue, improve performance, remove malware, unlock an account, or provide a free service. In return, the victim is asked to share credentials, install remote access software, approve MFA, or disclose sensitive information.

A realistic hypothetical example would be a caller contacting employees and saying, "This is IT support. We are upgrading email security today. I can keep your mailbox from being locked, but I need you to confirm the code that just appeared on your phone." This example is hypothetical, but it reflects a real attacker pattern: offering assistance while collecting authentication material.

Prevention should focus on verification and boundaries. Employees should verify unsolicited offers through official channels, never provide credentials or MFA codes in exchange for assistance, and contact the real IT support desk using known numbers or the approved ticketing system. Security awareness training should make clear that legitimate support staff should not ask for passwords, one-time codes, or secret recovery information.

## 6. Social Engineering Comparison Table

| Attack Type | Primary Target | Attack Channel | Psychological Lever Exploited | Typical Goal | Best Countermeasure |
| --- | --- | --- | --- | --- | --- |
| Phishing | General users and employees | Email, web links, messages | Trust, urgency, fear | Credential theft or malware delivery | Awareness training plus email filtering and MFA |
| Spear Phishing | Specific employees or teams | Email or business messaging | Trust, relevance, authority | Initial access to business systems | User reporting, least privilege, and targeted training |
| Whaling | Executives and finance leaders | Email, phone, messaging | Authority, urgency, pressure | Wire fraud or sensitive approval | Independent verification of executive requests |
| Vishing | Employees, help desks, customers | Phone calls or voice messages | Authority, fear, helpfulness | Password reset, MFA bypass, fraud | Verified callbacks and help desk procedures |
| Smishing | Mobile users and employees | SMS or mobile messaging | Urgency, fear, curiosity | Credential theft or malicious link clicks | Mobile awareness and link protection |
| Pretexting | Employees, vendors, support staff | Phone, email, chat, in person | Trust, authority, helpfulness | Sensitive information or account changes | Strong identity verification |
| Baiting | Employees and individual users | USB devices, downloads, ads | Curiosity, greed, free offer | Malware execution or credential theft | USB controls and trusted download policies |
| Quid Pro Quo | Users seeking help or benefits | Phone, email, chat, web forms | Helpfulness, trust, reward | Credentials, MFA codes, remote access | Official support channels and no-code-sharing rules |

## 7. Employee Security Awareness Training Checklist

1. Conduct regular phishing simulations with realistic scenarios. Organizations should test email, SMS, voice, and collaboration-platform lures that match current attacker behavior. Simulations are important because they help employees practice recognition and reporting in a controlled environment before a real attacker contacts them.

2. Train employees to verify identities and unusual requests. Staff should know how to confirm callers, vendors, executives, and support requests through approved channels. This matters because social engineering often succeeds when a request feels routine but is actually a fraud attempt.

3. Establish a clear suspicious activity reporting process. Organizations should provide an easy way to report suspicious emails, calls, texts, USB devices, and fake websites. Fast reporting gives security teams a chance to remove messages, block domains, warn other users, and investigate before the attack spreads.

4. Teach USB and download security. Employees should understand that unknown devices, pirated software, fake updates, and free tools can carry malware. This is important because baiting attacks may bypass email security and depend only on curiosity or convenience.

5. Conduct regular refresher training and measure awareness. Social engineering techniques change, so training should not be a one-time annual slide deck. Organizations should measure reporting rates, repeat risky patterns, and improve training based on real incidents and simulation results.

## 8. Conclusion

Social engineering remains effective because it fits into normal human behavior. People trust familiar brands, respond to authority, help others, react to urgent problems, and become curious about unexpected offers. Attackers understand these habits and design messages, calls, websites, and physical bait to push victims into quick decisions.

Humans are frequently targeted because they often control the doorway to technical systems. A password, reset approval, MFA prompt, downloaded file, or connected USB device can give an attacker the starting point needed for a larger intrusion. Technical controls alone are not enough because attackers can route around them by manipulating people and processes. At the same time, awareness alone is not enough either. The best defense combines trained employees with email filtering, phishing-resistant MFA, verified support procedures, least privilege, endpoint protection, application control, and clear reporting.

For employees, the key lesson is to slow down and verify unusual requests. For security teams, the lesson is to design systems that expect human mistakes and make reporting easy. For organizations, the lesson is to treat social engineering as a business risk, not only an IT problem. Strong security culture, layered controls, and quick incident response can reduce the chance that one convincing message or phone call becomes a serious breach.

## 9. References

1. Cybersecurity and Infrastructure Security Agency. "Avoiding Social Engineering and Phishing Attacks."
   https://www.cisa.gov/news-events/news/avoiding-social-engineering-and-phishing-attacks

2. National Institute of Standards and Technology. "SP 800-50 Rev. 1: Building a Cybersecurity and Privacy Learning Program."
   https://csrc.nist.gov/pubs/sp/800/50/r1/final

3. MITRE ATT&CK. "Phishing, T1566."
   https://attack.mitre.org/techniques/T1566/

4. MITRE ATT&CK. "Phishing: Spearphishing Attachment, T1566.001."
   https://attack.mitre.org/techniques/T1566/001/

5. New York State Department of Financial Services. "Twitter Investigation Report."
   https://www.dfs.ny.gov/reports-and-publications/other-reports/Twitter_Report

6. X / Twitter. "An update on our security incident."
   https://blog.x.com/en_us/topics/company/2020/an-update-on-our-security-incident

7. Verizon. "2024 Data Breach Investigations Report."
   https://www.verizon.com/business/resources/reports/dbir/

8. CISA. "CISA Releases Guidance on Phishing-Resistant and Numbers Matching Multifactor Authentication."
   https://content.govdelivery.com/accounts/USDHSCISA/bulletins/3355d59

9. NIST. "Digital Identity Guidelines: Authenticators - Phishing Resistance."
   https://pages.nist.gov/800-63-4/sp800-63b/authenticators/

10. Mandiant / Google Cloud. "Why Are You Texting Me? UNC3944 Leverages SMS Phishing Campaigns for SIM Swapping, Ransomware, Extortion, and Notoriety."
    https://cloud.google.com/blog/topics/threat-intelligence/unc3944-sms-phishing-sim-swapping-ransomware/

11. CISA. "Scattered Spider Cybersecurity Advisory AA23-320A."
    https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-320a

12. Mandiant / Google Cloud. "FIN7 Power Hour: Adversary Archaeology and the Evolution of FIN7."
    https://cloud.google.com/blog/topics/threat-intelligence/evolution-of-fin7

13. UCLA Office of the Chief Information Security Officer. "The FIN7 Cyber Actors Targeting US Businesses through USB Keystroke Injection Attacks."
    https://ociso.ucla.edu/news/fin7-cyber-actors-targeting-us-businesses-through-usb-keystroke-injection-attacks

14. CISA. "Primary Stuxnet Advisory."
    https://www.cisa.gov/uscert/ics/advisories/ICSA-10-272-01
