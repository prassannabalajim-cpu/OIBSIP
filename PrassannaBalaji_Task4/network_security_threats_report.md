# Research Report: Common Network Security Threats

## 1. Introduction

Network security threats matter because nearly every modern organization depends on connected systems to serve customers, communicate with staff, process payments, access cloud services, and store business information. A weakness in the network can affect confidentiality by exposing private data, integrity by allowing unauthorized changes to information, and availability by making systems unreachable when people need them. These three security goals are connected: an outage can stop business operations, stolen credentials can lead to data tampering, and manipulated network traffic can damage trust in a service. Since organizations now rely on internet-facing applications, remote access, wireless networks, third-party platforms, and distributed infrastructure, network security cannot be treated as a one-time configuration task. It has to be proactive, monitored, and layered so that attacks are detected early and one failed control does not lead to a complete compromise.

## 2. Denial-of-Service (DoS/DDoS) Attacks

### 2.1 How the Attack Works

A Denial-of-Service attack is an attempt to make a system, application, or network unavailable to legitimate users. The attacker may overload a server with traffic, consume connection tables, exhaust CPU or memory, or abuse an expensive application function until the service can no longer respond normally. A Distributed Denial-of-Service attack has the same goal, but the traffic comes from many systems at the same time. That difference is important because a single attacking host can often be blocked, while a distributed attack may involve thousands of unrelated source addresses spread across many networks.

In many DDoS attacks, the attacker controls a botnet. A botnet is a group of compromised devices that receive commands from the attacker. The devices may be home routers, cameras, poorly secured servers, or infected computers. The owner of each device may not know that the device is participating in an attack. When the attacker sends a command, the bots begin sending packets or application requests toward the victim.

Traffic flooding works by creating more work than the target or its upstream network can handle. In a SYN flood, the attacker sends many TCP SYN packets and tries to consume the victim's half-open connection resources. In a UDP flood, the attacker sends large amounts of UDP traffic to random or selected ports, forcing the victim to process packets or respond with unreachable messages. In an HTTP flood, bots send large numbers of web requests that look more like normal user activity, which can make filtering harder. In amplification attacks, the attacker sends small requests to third-party servers while spoofing the victim's IP address. The third-party servers then send larger replies to the victim, multiplying the attack traffic.

```text
Attacker command
      |
      v
Compromised devices across the internet
      |
      v
Large traffic volume toward one target
      |
      v
Service slowdown or outage for real users
```

### 2.2 Real-World Example

A major example is the October 21, 2016 DDoS attack against Dyn, a managed DNS provider. Dyn's own incident summary described the event as a complex DDoS attack against its Managed DNS infrastructure using traffic over port 53, including TCP and UDP traffic. Because many well-known websites depended on Dyn for DNS resolution, users had trouble reaching services even when the services themselves were not necessarily down.

The attack was significant because it showed how insecure Internet of Things devices could be turned into internet-scale attack infrastructure. Mirai malware scanned for devices such as cameras, DVRs, routers, and other connected equipment that still used weak or default credentials. Once compromised, those devices became bots that could be directed to flood a target. Krebs on Security reported on Mirai's role in some of the largest attacks of that period, and Wired reported that the Dyn disruption affected services such as Twitter, Spotify, Reddit, Netflix, PayPal, and Slack.

The Dyn incident also exposed a dependency problem. DNS is a basic internet function: if users cannot resolve a domain name, the application may appear down even if its web servers are running. The attack therefore did not only affect one company. It caused visible disruption across many online services and made the security of consumer IoT devices a business continuity issue for the wider internet.

### 2.3 Impact

The most direct impact of a DoS or DDoS attack is loss of availability. Customers cannot log in, employees cannot access hosted systems, APIs fail, and normal business activity slows down. For online businesses, even a short outage can mean lost sales, missed service-level commitments, and support backlogs.

The financial impact can include incident response costs, emergency DDoS mitigation services, overtime for technical teams, and lost revenue during downtime. Reputation also suffers because customers may not distinguish between a network attack and poor service reliability. A company that is repeatedly unavailable can lose trust, especially if customers depend on it for payments, healthcare, logistics, education, or government services.

DDoS attacks also consume incident response resources. Network engineers, security analysts, support teams, management, vendors, and internet service providers may all become involved. During a large attack, teams may have to separate malicious traffic from legitimate traffic under pressure, update filtering rules, communicate with customers, and preserve evidence for later review.

### 2.4 Mitigation Strategies

One important mitigation is DDoS protection with traffic filtering. Specialized DDoS protection services analyze packet fields, request metadata, traffic rates, and known attack patterns. When attack traffic is identified, it can be dropped, challenged, rate-limited, or scrubbed before it reaches the protected origin. This works best when filtering happens close to the network edge because the attack traffic is removed before it consumes the victim's local bandwidth.

Rate limiting and traffic monitoring are also necessary. Rate limiting sets reasonable thresholds for requests from a source, session, network, or route. It is especially useful against application-layer floods, login abuse, and API exhaustion. Monitoring provides the visibility needed to recognize unusual traffic patterns, such as sudden spikes in SYN packets, abnormal DNS query volume, or high error rates from specific endpoints. Without monitoring, defenders may not know whether they are seeing a real attack, a flash crowd, or a broken client.

Redundant and distributed infrastructure reduces the chance that one overloaded location becomes a complete outage. CDNs, anycast routing, load balancing, multiple regions, and secondary DNS providers can spread traffic across more capacity. This does not make an organization immune to DDoS, but it gives defenders more room to absorb traffic, reroute users, and keep critical services reachable while mitigation rules are applied.

## 3. Man-in-the-Middle (MITM) Attacks

### 3.1 How the Attack Works

A Man-in-the-Middle attack occurs when an attacker positions themselves between two communicating parties and intercepts their traffic. Depending on the protocol and the attacker's level of control, the attacker may only observe traffic, or they may modify messages before forwarding them. Modern security literature often uses the term adversary-in-the-middle because the attacker is not always literally in the physical middle; they may control a router, access point, DNS setting, proxy, or local network path.

On a local network, ARP spoofing is a common technique. ARP maps an IPv4 address to a MAC address on a local segment. Because ARP was not designed with strong authentication, an attacker can send false ARP messages that make a victim believe the attacker's machine is the gateway. The victim then sends traffic through the attacker. MITRE ATT&CK tracks this as ARP Cache Poisoning under the Adversary-in-the-Middle technique.

Rogue Wi-Fi and Evil Twin attacks use wireless access instead of ARP. In an Evil Twin attack, the attacker creates a fake Wi-Fi network that looks like a trusted network, often by using the same or a similar SSID. Users may connect because the network name looks familiar or has a stronger signal. Once connected, the attacker can observe DNS requests, redirect users to fake login pages, attempt downgrade attacks, or capture traffic that is not properly encrypted. MITRE ATT&CK also documents Evil Twin as an adversary-in-the-middle sub-technique.

DNS manipulation can also support MITM attacks. If an attacker changes a router's DNS settings, poisons a DNS response, or controls a malicious resolver, a victim may be sent to an attacker-controlled server while believing they are visiting a legitimate site.

```text
Normal path:
User device ---> Legitimate gateway ---> Real service

MITM path:
User device ---> Attacker-controlled point ---> Real or fake service
```

### 3.2 Real-World Example

A useful documented example is the U.S. Department of the Interior Office of Inspector General wireless security audit published in 2020. The OIG tested Department wireless networks using portable equipment from publicly accessible areas and simulated attacks such as eavesdropping, Evil Twin access points, and password cracking. The report found that the attacks went undetected and that testers were able to intercept and decrypt wireless network traffic in multiple bureaus.

This example is not a criminal breach report, but it is a credible real-world assessment by a government oversight body. It shows why wireless MITM risk is practical rather than theoretical. Attack equipment can be small, inexpensive, and close to the victim. If monitoring, segmentation, certificate validation, and wireless security practices are weak, an attacker near a building, hotel, airport, or office may be able to collect sensitive traffic or credentials.

Another recent example of MITM-related activity is the 2026 U.S. Department of Justice announcement about disruption of a DNS hijacking network linked to Russian military intelligence. According to the announcement, compromised routers were used to redirect DNS requests to malicious resolvers, and selected targets received fraudulent DNS records that supported actor-in-the-middle attacks against encrypted traffic. This illustrates how control of network infrastructure can be used to set up interception even when the victim thinks normal DNS resolution is taking place.

### 3.3 Impact

The impact of MITM attacks is mainly related to confidentiality and integrity. If traffic is not encrypted, credentials, session cookies, personal information, business documents, and internal system details may be exposed. If the attacker can modify traffic, they may inject malware, change payment instructions, alter downloaded files, or redirect users to phishing pages.

Session hijacking is another serious risk. If an attacker captures a valid session token, they may impersonate the user without knowing the password. Financial fraud can occur when attackers alter banking sessions, payment destinations, invoices, or login pages. Even when strong encryption protects the content, MITM positioning can still provide useful metadata, such as which services a user is accessing and when.

### 3.4 Mitigation Strategies

HTTPS with strong TLS encryption reduces MITM risk by protecting data in transit between the client and the real server. If TLS is configured correctly, an attacker who can see the packets should still be unable to read or change the protected content. Organizations should disable obsolete protocol versions and weak cipher suites, use HSTS where appropriate, and ensure internal applications also use encryption rather than relying only on perimeter controls.

Proper certificate validation is just as important as encryption. Users and applications should reject invalid, expired, mismatched, or untrusted certificates. Many MITM attacks depend on convincing a user to accept a certificate warning or forcing an application to skip validation. Certificate pinning, managed trust stores, and clear handling of TLS errors can reduce this risk for sensitive applications.

Network security controls help stop the attacker from gaining a middle position. DHCP snooping can prevent unauthorized DHCP servers from assigning malicious gateways or DNS servers. Dynamic ARP inspection can reject suspicious ARP replies on managed switches. Secure Wi-Fi using WPA2-Enterprise or WPA3-Enterprise makes it harder to impersonate a corporate wireless network. Network segmentation limits the damage if a user connects to a hostile network because the attacker does not automatically gain access to every internal service.

## 4. IP Spoofing

### 4.1 How the Attack Works

IP spoofing is the practice of forging the source IP address in an IP packet. In normal traffic, the source address identifies where the reply should go. In spoofed traffic, the attacker writes a different source address into the packet header. This can hide the attacker's real address, impersonate another system, or cause replies to be sent to a victim.

A simple example is shown below:

```text
Normal packet:
Source IP: 203.0.113.10       Destination IP: 198.51.100.20

Spoofed packet:
Source IP: 198.51.100.99      Destination IP: 192.0.2.50
Actual sender: 203.0.113.10
```

Attackers use spoofing because many network protocols trust the source address enough to send a response. In reflection attacks, the attacker sends a request to a third-party server but spoofs the victim's IP as the source. The third-party server replies to the victim. In amplification attacks, the response is much larger than the request, so the victim receives more traffic than the attacker had to send.

Spoofing can also make attribution harder. A defender may see the forged source IP in packet logs and initially believe that address is responsible. However, because the source is fake, investigation usually requires help from upstream providers and packet-path analysis.

### 4.2 Real-World Example

CISA's alert on UDP-based amplification attacks describes distributed reflective denial-of-service attacks that rely on public UDP services and spoofed source IP addresses. UDP does not validate the source address as part of a connection setup, so attackers can forge the victim's IP address in requests to exposed services. Those services then send replies to the victim. CISA lists DNS, NTP, LDAP, SSDP, SNMP, memcached, and other UDP-based protocols as possible amplification vectors when exposed or misconfigured.

This is a strong example because it shows IP spoofing as an enabling technique rather than as an isolated attack. The attacker may not need to compromise the reflector. Instead, they abuse normal server behavior and poor source address filtering elsewhere on the internet.

### 4.3 Impact

IP spoofing supports reflection and amplification attacks by causing innocent third-party servers to send traffic to the victim. This can increase the scale of a DDoS attack and make it harder for the victim to block traffic because packets appear to come from many legitimate services.

Spoofing can also support identity impersonation in environments that still trust IP addresses too much. For example, a legacy system may allow access from a trusted IP range without requiring strong authentication. If routing and network controls allow forged packets, that trust model can be abused.

Another impact is difficulty in attack attribution. Logs may contain source addresses that are not the real origin. Security teams may spend time investigating innocent systems or reflectors instead of the attacker. This is one reason source address validation is considered an internet-wide operational responsibility.

### 4.4 Mitigation Strategies

Ingress and egress filtering reduce spoofing by checking whether packets use source addresses that make sense for the network path. Ingress filtering blocks packets entering a network with invalid or unexpected source addresses. Egress filtering blocks packets leaving a network if their source address does not belong to that network's assigned range. Together, these controls stop networks from accepting or sending obviously forged packets.

Source address validation and BCP 38 are important operational practices. BCP 38, documented in RFC 2827, recommends filtering traffic with spoofed source addresses near the edge of the network. MANRS also treats anti-spoofing as a core network operator action. The idea is simple: the closer filtering happens to the source, the less spoofed traffic reaches the wider internet.

Organizations should avoid IP-only authentication. IP allowlists can be useful as one layer, but they should not replace strong authentication, authorization, encryption, and logging. Administrative interfaces, APIs, remote access systems, and internal services should require credentials, certificates, tokens, or other controls that do not rely only on the apparent source IP address.

## 5. DNS Poisoning/Spoofing

### 5.1 How the Attack Works

The Domain Name System translates human-readable names, such as `example.com`, into IP addresses that computers use for network communication. A typical DNS lookup starts when a user's device asks a resolver for a domain. If the resolver does not already have a cached answer, it queries other DNS servers until it receives the needed record, then returns the answer to the client and may cache it for later use.

DNS poisoning is an attack where false DNS information is inserted into a resolver's cache. DNS spoofing is a broader term for sending or presenting a forged DNS response. In both cases, the goal is to make the victim use the wrong IP address for a domain. A user may type the correct domain name but be sent to a malicious server.

```text
User asks: Where is bank.example?
Attacker-forged answer: 198.51.100.66
Result: User visits attacker-controlled system instead of the real site
```

Attackers may manipulate DNS responses by racing the legitimate DNS answer, exploiting weak randomness in transaction IDs or source ports, compromising DNS settings on a router, or controlling a malicious resolver. If the forged answer is cached, many users who depend on that resolver may be affected until the cache expires or is cleared.

### 5.2 Real-World Example

The 2008 Kaminsky DNS cache poisoning vulnerability is one of the best-known DNS security incidents. CERT/CC Vulnerability Note VU#800113 explained that weaknesses in DNS protocol behavior and implementations made cache poisoning practical against caching resolvers. The issue involved factors such as limited transaction ID space, predictable behavior in some implementations, multiple outstanding requests, and fixed or insufficiently randomized source ports.

The significance was not limited to one vendor. Multiple DNS implementations were affected, and many vendors released coordinated patches. The immediate mitigation was source port randomization, which made it harder for attackers to guess the correct combination needed to inject a forged response. The incident also increased attention on DNSSEC because DNSSEC can provide cryptographic validation that DNS responses are authentic.

### 5.3 Impact

DNS poisoning can lead to phishing because users may be redirected to a site that looks legitimate while the address bar still shows the expected domain. If users enter credentials, the attacker can steal them. It can also support malware distribution by sending software update requests or download links to malicious infrastructure.

Website redirection can disrupt business operations and damage trust. Customers may believe a company has been hacked even if the problem is at a resolver or network provider. Email and other services can also be affected if DNS records are manipulated. For organizations, DNS integrity is directly tied to brand trust and reliable service delivery.

### 5.4 Mitigation Strategies

DNSSEC helps by adding cryptographic signatures to DNS data. A validating resolver can check whether a DNS answer is authentic and has not been altered. DNSSEC does not encrypt DNS traffic, but it does protect integrity, which is the key issue in cache poisoning.

Secure DNS server configuration and regular patching are also essential. Resolvers should use strong transaction ID and source port randomization, restrict recursion to authorized clients, avoid operating as open resolvers, and apply vendor security updates. The Kaminsky case showed that implementation details can decide whether a theoretical DNS issue becomes easy to exploit.

DNS monitoring and anomaly detection help identify suspicious behavior. Defenders can monitor for unusual DNS response patterns, sudden changes in records, unexpected resolver settings, spikes in NXDOMAIN responses, and traffic to newly observed malicious domains. Monitoring is especially useful because DNS attacks may not immediately look like endpoint malware; users simply resolve a name and go where the resolver sends them.

## 6. Threat Comparison

| Threat | Attack Vector | Primary Security Impact | Who Is at Risk? | Difficulty to Execute | Ease of Mitigation |
| --- | --- | --- | --- | --- | --- |
| DoS/DDoS | Traffic floods, protocol abuse, botnets, reflection, amplification | Availability | Public websites, DNS providers, APIs, online services, network operators | Medium to High | Medium |
| MITM | ARP spoofing, rogue Wi-Fi, Evil Twin access points, DNS manipulation, malicious proxies | Confidentiality and integrity | Public Wi-Fi users, enterprise LANs, remote workers, mobile users | Medium | Medium |
| IP Spoofing | Forged source IP addresses in packets | Availability and attribution integrity | DDoS targets, reflectors, ISPs, legacy trusted networks | Medium | Medium to High |
| DNS Poisoning | Forged DNS responses, resolver cache poisoning, malicious DNS settings | Integrity and confidentiality | DNS resolvers, enterprises, customers, website visitors | Medium to High | Medium |

## 7. Key Takeaways for Network Administrators

1. Continuous monitoring and early detection are essential. Network administrators need visibility into traffic volume, DNS behavior, wireless activity, routing changes, and authentication events. Early detection gives teams time to filter traffic, isolate affected systems, and contact providers before a minor incident becomes a public outage.

2. Defense-in-depth is stronger than depending on one control. TLS, DDoS filtering, segmentation, DNSSEC, secure Wi-Fi, source address validation, and strong authentication solve different parts of the problem. Layered controls are important because attackers often chain techniques, such as DNS manipulation followed by credential theft.

3. Secure configuration and regular patching reduce avoidable exposure. Many network attacks succeed because of default credentials, open resolvers, outdated firmware, weak wireless settings, or legacy trust rules. Administrators should maintain asset inventories, harden network devices, patch DNS and router software, and regularly test whether controls still work.

## 8. Conclusion

Common network security threats affect different parts of the security model. DoS and DDoS attacks mainly target availability by preventing real users from reaching systems. MITM attacks threaten confidentiality and integrity by giving an attacker access to traffic between trusted parties. IP spoofing can hide the source of traffic and enable reflection attacks, while DNS poisoning can redirect users even when they type the correct domain name. Understanding these differences helps defenders choose the right controls instead of treating all network threats the same way.

The strongest security programs use layered defenses. Traffic filtering, monitoring, resilient infrastructure, TLS, certificate validation, secure switching features, source address validation, DNSSEC, and regular patching all play different roles. No single tool can prevent every attack, but a proactive approach makes attacks harder to execute and easier to detect. For network administrators, the main lesson is that reliable networks require both good design and daily operational discipline.

## 9. References

1. National Institute of Standards and Technology. "SP 800-12 Rev. 1: An Introduction to Information Security." https://csrc.nist.gov/pubs/sp/800/12/r1/final
2. Cybersecurity and Infrastructure Security Agency. "UDP-Based Amplification Attacks." https://www.cisa.gov/ncas/alerts/ta14-017a
3. MITRE ATT&CK. "Adversary-in-the-Middle: ARP Cache Poisoning, T1557.002." https://attack.mitre.org/techniques/T1557/002/
4. MITRE ATT&CK. "Adversary-in-the-Middle: Evil Twin, T1557.004." https://attack.mitre.org/techniques/T1557/004/
5. CERT Coordination Center. "VU#800113: Multiple DNS implementations vulnerable to cache poisoning." https://www.kb.cert.org/vuls/id/800113
6. Dyn. "Dyn Analysis Summary Of Friday October 21 Attack." https://postmortem.io/incidents/dyn--2016-10-21--managed-dns-ddos-mirai-attack/
7. Krebs on Security. "Mirai IoT Botnet Co-Authors Plead Guilty." https://krebsonsecurity.com/2017/12/mirai-iot-botnet-co-authors-plead-guilty/
8. Wired. "The Mirai Botnet Was Part of a College Student 'Minecraft' Scheme." https://www.wired.com/story/mirai-botnet-minecraft-scam-brought-down-the-internet/
9. U.S. Department of the Interior Office of Inspector General. "Evil Twins, Eavesdropping & Password Cracking: How OIG Successfully Attacked DOI's Wireless Networks." https://www.doioig.gov/reports/audit/evil-twins-eavesdropping-password-cracking-how-oig-successfully-attacked-dois-0
10. U.S. Department of Justice. "Justice Department Conducts Court-Authorized Disruption of DNS Hijacking Network Controlled by a Russian Military Intelligence Unit." https://www.justice.gov/usao-edpa/pr/justice-department-conducts-court-authorized-disruption-dns-hijacking-network
11. MANRS. "MANRS Implementation Guide for Network Operators." https://manrs.org/netops/guide/
12. Cloudflare Docs. "How DDoS protection works." https://developers.cloudflare.com/ddos-protection/about/how-ddos-protection-works/
