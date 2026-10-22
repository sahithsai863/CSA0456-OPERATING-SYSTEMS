Cybersecurity Report Analysis – Assignment Answers
The following answers are structured according to the given rubrics: Report Analysis and Interpretation, Identification of Security Risks and Vulnerabilities, Application of Cybersecurity Concepts and Countermeasures, and Technical Communication and Documentation. Each answer includes technical justification and practical security recommendations appropriate to the marks allotted.
1. Network Security Assessment Using Nmap (20 Marks)
1.1 Introduction and Report Analysis
Nmap (Network Mapper) is a network scanning tool used to identify active hosts, open ports, running services, service versions, and operating systems. It helps security analysts identify potential attack surfaces and assess whether network services are appropriately secured. � �
nmap.org
nmap.org
In this scenario, the security analyst scanned the target system 192.168.1.10 and identified the following open ports:
Port
Service
Primary function
Main security concern
22/TCP
SSH
Secure remote administration
Weak credentials and insecure configuration
80/TCP
HTTP
Web access
Unencrypted traffic and web application vulnerabilities
3306/TCP
MySQL
Database communication
Unauthorized database access and data exposure
The report also identifies the operating system and service versions. This information is useful for security auditing, but it can also help attackers select suitable attack techniques against outdated or vulnerable software.
Important observation: The address 192.168.1.10 is a private network address. The scan proves that these services were reachable from the scanner's location; it does not, by itself, prove that they are accessible directly from the public internet.
1.2 Security Risks and Possible Attack Vectors
A. HTTP – Port 80
HTTP is commonly used to deliver web pages and application content. Ordinary HTTP does not encrypt traffic between a client and a server, creating a risk when sensitive information is transmitted over it.
Security risks:
Unencrypted communication: Login details, session cookies, or other sensitive information transmitted over HTTP may be exposed to interception or modification by an attacker positioned to observe or manipulate the traffic.
Web application vulnerabilities: Poorly secured applications may contain SQL injection, cross-site scripting (XSS), broken access controls, or file-handling vulnerabilities.
Outdated software: An old web server, content management system, or application component may contain publicly documented vulnerabilities.
Information disclosure: Error messages, server banners, and exposed directories may reveal details useful for further reconnaissance.
Possible attack scenario: An attacker with network access discovers that the web application is running an outdated component. The attacker investigates whether a known vulnerability applies and, if the weakness is present, may attempt to access restricted application data or execute unintended actions.
Countermeasures:
Redirect HTTP traffic to HTTPS and enforce TLS using a valid certificate.
Update the web server, frameworks, and application components.
Apply secure coding practices, including parameterized SQL queries, input validation, and access-control checks.
Use a web application firewall (WAF) where appropriate, alongside regular vulnerability assessments.
Disable directory listing, remove unnecessary server banners, and monitor application logs.
B. SSH – Port 22
SSH provides encrypted remote access for administrators. However, exposing it to unnecessary networks or using weak authentication can make it a target for unauthorized access.
Security risks:
Brute-force attacks: Attackers repeatedly attempt password combinations to gain access.
Credential reuse: Passwords stolen from another service may be tried against SSH accounts.
Weak configuration: Outdated SSH software or obsolete cryptographic settings may increase the risk of compromise.
Excessive privileges: Compromising an administrator account can provide extensive control over the target system.
Possible attack scenario: An attacker identifies an SSH service and attempts to log in using leaked credentials or weak passwords. If authentication succeeds and the account has excessive privileges, the attacker may access sensitive files, modify configurations, or move to other systems.
Countermeasures:
Prefer SSH public-key authentication and disable password authentication where operationally feasible.
Disable direct root login and use named accounts with least privilege.
Restrict SSH access through firewalls, VPNs, or trusted-source IP allowlists.
Enforce multifactor authentication where supported.
Update SSH software, remove obsolete algorithms, apply login rate limits, and monitor failed login attempts.
Changing the SSH port alone is not a sufficient security measure; authentication and network-access restrictions are more important.
C. MySQL – Port 3306
MySQL is a relational database management system commonly used to store application data, user credentials, transaction details, and business records. Its exposure is particularly concerning when database access is allowed from untrusted networks.
Security risks:
Unauthorized database access: Attackers may try default, weak, leaked, or reused database credentials.
Sensitive data exposure: A compromised account may allow access to customer records, personal information, or business data.
Database manipulation: Excessive privileges may enable unauthorized modification or deletion of records.
Known software vulnerabilities: Outdated database versions may contain exploitable security flaws.
Application-to-database compromise: If a web application is vulnerable and uses an overprivileged database account, an application-level compromise may cause greater damage.
Possible attack scenario: An attacker finds that MySQL accepts connections from an unnecessarily broad range of hosts. If the attacker also obtains valid credentials or exploits a verified vulnerability, the attacker may retrieve or alter data according to the access granted.
An open MySQL port alone does not prove that the database is vulnerable or that its contents can be accessed without authentication.
Countermeasures:
Block external access to port 3306 and permit connections only from authorized application servers or administration hosts.
Bind MySQL to the required internal interface instead of exposing it on every interface.
Use strong, unique credentials and separate accounts for applications, administrators, and reporting tasks.
Apply the principle of least privilege and avoid using database administrator accounts for normal application operations.
Patch MySQL, enable encrypted connections where appropriate, log suspicious access, and maintain tested backups. � �
cheatsheetseries.owasp.org
cheatsheetseries.owasp.org
1.3 Risk Prioritization
Priority
Finding
Reason
Critical to high, depending on exposure
MySQL accessible from an untrusted network
Could expose or compromise sensitive database records
High, depending on configuration
SSH accessible with weak authentication
May allow unauthorized administrative access
Medium to high, depending on application weaknesses
HTTP service
May expose traffic or provide a route through vulnerable application functions
Assessment required
OS and service versions disclosed
Can help attackers identify applicable known vulnerabilities
These are preliminary priorities. The actual severity depends on reachability, software versions, authentication controls, data sensitivity, and whether a vulnerability is confirmed.
1.4 Overall Recommendations and Conclusion
The analyst should first verify the installed service versions and check them against vendor security advisories. Unnecessary services should be disabled, while required services should be restricted to authorized networks. HTTP should redirect to HTTPS, SSH should use strong authentication and restricted access, and MySQL should normally be accessible only to approved application and administration hosts.
Firewall configuration, secure patch management, least privilege, centralized logging, vulnerability scanning, and regular penetration testing should be incorporated into the organization's security program.
Conclusion: The Nmap report identifies a potentially significant attack surface. The most important action is to restrict database exposure, harden SSH authentication, secure the web application, and validate any suspected software vulnerabilities. These actions reduce the likelihood of unauthorized access, data theft, and system compromise.
2. Phishing Awareness Assessment Using GoPhish (20 Marks)
2.1 Introduction and Report Analysis
GoPhish is a phishing-simulation platform used to conduct authorized security-awareness exercises and evaluate how employees respond to suspicious emails.
The assessment at ABC Technologies Pvt. Ltd. produced the following results:
Report finding
Result
Security implication
Employees clicked the phishing link
40%
A significant portion interacted with a suspicious link
Employees entered login credentials
20%
Credentials could be exposed to an attacker in a real incident
Employees downloaded a malicious attachment
Several users
Possible endpoint compromise, depending on whether the file was opened or executed
The results indicate weaknesses in phishing recognition, safe handling of login requests, and attachment verification. The credential-submission percentage should be interpreted according to the report's denominator; the available information does not establish whether the 20% represents all recipients or only those who clicked.
A download also does not automatically mean malware executed. However, it is a serious warning that requires investigation.
2.2 Identification of Employee Security Weaknesses
A. Insufficient recognition of suspicious links
The 40% click rate suggests that many employees may not consistently verify the sender, inspect links, or question unexpected messages.
Attackers often use urgency, authority, curiosity, or familiar branding to make phishing messages appear genuine.
Risk: Employees may visit fraudulent websites, download harmful content, or be redirected to counterfeit login pages.
B. Unsafe handling of credentials
The 20% credential-submission rate suggests that some employees trusted a link and submitted sensitive information without verifying the destination.
Risk: Attackers could use stolen credentials to access corporate email, cloud applications, VPNs, or other systems. Reused passwords could increase the potential impact.
Multifactor authentication (MFA), especially phishing-resistant methods, can reduce the risk that a stolen password alone is sufficient for account access. � �
cisa.gov
cisa.gov
C. Unsafe attachment handling
Several users downloaded a malicious attachment, indicating that attachment safety checks may be inadequate.
Risk: If a downloaded file is opened or executed, it could install malware, steal information, establish unauthorized access, or contribute to ransomware deployment.
D. Inadequate reporting behavior
The report does not provide the number of employees who reported the suspicious messages. ABC Technologies should measure this separately.
If employees do not report suspicious emails, security teams may learn about attacks only after credentials are stolen or an endpoint is compromised.
2.3 Recommended User Awareness Programs
A. Regular security-awareness training
ABC Technologies should conduct compulsory training at onboarding and refresher sessions at regular intervals. Training should include:
Identifying suspicious sender addresses, misleading domains, unusual requests, and unexpected attachments.
Recognizing urgency, threats, financial requests, and requests for confidential information.
Verifying sensitive requests through an independently obtained phone number or another trusted communication channel.
Avoiding login through unexpected email links and navigating to services through known, trusted addresses.
Reporting suspicious messages immediately using the organization's approved reporting mechanism.
B. Controlled phishing simulations
The organization should conduct periodic GoPhish exercises using different scenarios, such as fake document-sharing notifications, password-expiry messages, and invoice requests.
Training should be provided after a simulation, especially for employees who clicked, submitted credentials, or downloaded a file. The objective should be to improve behavior rather than shame or punish employees for a learning exercise.
Simulations should be authorized, limited in scope, respectful of employee privacy, and designed not to collect real passwords or deploy actual malware.
C. Measure and improve performance
Track the click rate, credential-submission rate, attachment interaction rate, reporting rate, and time taken to report. Compare these indicators across campaigns to determine whether training and technical controls are effective.
CISA recommends combining user awareness with technical protections, including multifactor authentication, email filtering, and processes for identifying and reporting phishing. � �
cisa.gov
cisa.gov
2.4 Recommended Email Security Controls
Security control
Application and benefit
Secure email gateway
Filters suspicious messages, known malicious URLs, spam, and risky attachments before delivery
SPF, DKIM, and DMARC
Help validate authorized sending sources and reduce domain spoofing when correctly configured
URL scanning and protection
Checks suspicious links and may block access when a destination is identified as malicious
Attachment analysis and sandboxing
Detects or isolates potentially harmful files before users can interact with them
Attachment restrictions
Blocks unnecessary high-risk file types and reduces unsafe attachment delivery
External email warning
Helps employees recognize messages originating outside the organization
Phishing-resistant MFA
Reduces the impact of password theft by adding stronger authentication protection
Endpoint detection and response (EDR)
Helps detect suspicious processes, malware, and potential endpoint compromise
Email protection should combine multiple controls rather than relying on a single filter. CISA's guidance highlights attachment filtering, email monitoring, and other measures to reduce successful phishing attacks. � � �
cisa.gov
cisa.gov
cisa.gov
2.5 Recommended Organizational Policies
ABC Technologies should implement the following policies:
Email and attachment policy: Employees must verify unexpected files and requests before interacting with them.
Credential protection policy: Employees must never disclose passwords through email, report suspicious login pages, use unique passwords, and follow approved MFA procedures.
Incident reporting policy: Provide a simple method to report suspicious messages immediately, with clear instructions for anyone who clicks a link, submits credentials, or opens a suspicious file.
Access-control policy: Apply least privilege so that a compromised employee account cannot automatically access critical systems.
Incident response policy: Establish procedures for revoking sessions, resetting exposed credentials, investigating suspicious logins, and isolating potentially compromised endpoints.
Training and accountability policy: Provide periodic awareness training and use simulation results to identify training needs and improve controls.
Immediate action if this were a real incident
If the reported events involved real malicious content rather than a controlled simulation, security staff should investigate downloaded files and endpoint activity, reset exposed credentials, revoke suspicious sessions, and review authentication logs. Potentially infected devices should be isolated when appropriate while evidence is preserved.
2.6 Conclusion
The GoPhish report demonstrates that ABC Technologies faces a meaningful risk from phishing and social engineering. The click rate indicates weaknesses in link verification, credential submission indicates possible account compromise, and malicious attachment downloads raise concerns about endpoint security.
The organization should combine regular awareness training, controlled phishing simulations, secure email gateways, attachment and URL analysis, phishing-resistant MFA, and clear reporting procedures. The main objective is to build a security-aware workforce supported by technical controls, rather than relying on employees alone to prevent phishing attacks.
3. DNS Security Assessment Using the Dig Tool (10 Marks)
3.1 Introduction and Report Analysis
The dig tool (Domain Information Groper) is a command-line utility used to query DNS servers and examine DNS records. It can also be used during an authorized assessment to determine whether a DNS server permits an AXFR request.
A DNS zone transfer allows DNS data to be copied between primary and secondary DNS servers. An AXFR (Authoritative Zone Transfer) transfers the full DNS zone, rather than only selected records. This is legitimate when performed by authorized secondary DNS servers, but a transfer permitted to unauthorized requesters can disclose an organization's DNS information. � �
developers.cloudflare.com
bind9.readthedocs.io
In this scenario, the DNS assessment reveals that an unauthorized requester can successfully perform an AXFR transfer and obtain internal hostnames, mail server names, and other DNS records.
This finding indicates an access-control misconfiguration in the DNS infrastructure.
3.2 Security Implications and Risks
A. Information disclosure
The transferred records may identify:
Internal or sensitive hostnames, such as administrative or development systems.
Mail servers and associated mail-related DNS records.
Subdomains and IP addresses that reveal aspects of the organization's network structure.
Other DNS names that help explain relationships between organizational services.
This information can provide attackers with a more detailed picture of the organization's infrastructure.
B. Reconnaissance and targeted attacks
An attacker could use the exposed hostnames and IP addresses to prioritize further investigation of systems that should be checked only through authorized security testing.
For example, an exposed administrative hostname could help an attacker identify a potentially valuable target. If that system also has a separate, exploitable vulnerability or weak access controls, the DNS information could make the attack more targeted.
C. Increased phishing risk
Mail server names, subdomains, and other organizational naming conventions can assist attackers in creating convincing phishing messages or impersonating internal services.
D. Discovery of forgotten or poorly maintained systems
A zone transfer might reveal development, testing, or legacy hostnames that are no longer actively monitored. These systems may need additional verification to determine whether they are exposed, outdated, or still required.
Technical clarification: A successful AXFR does not, by itself, provide login credentials, grant access to the listed systems, or allow the attacker to modify DNS records. It is primarily an information-disclosure weakness that can support additional attacks.
3.3 Recommended DNS Security Measures
1. Restrict zone transfers
Configure the authoritative DNS server to permit zone transfers only to approved secondary DNS servers. Transfers should not be permitted to arbitrary clients.
For example, BIND DNS supports the allow-transfer access-control setting to specify which hosts can receive zone information. � �
bind9.readthedocs.io
bind9.readthedocs.io
2. Implement TSIG authentication
Use Transaction SIGnature (TSIG) keys to authenticate authorized DNS peers participating in zone transfers. Shared secrets must be securely generated, stored, rotated, and protected.
3. Apply firewall restrictions
Restrict DNS zone-transfer traffic to approved server addresses and necessary network paths. Firewall rules should support legitimate DNS operation without allowing unrestricted transfer requests.
4. Separate public and internal DNS information
Use an appropriate split-DNS architecture when internal records should not be publicly visible. Public-facing DNS zones should contain only the records necessary for public services.
However, separating zones does not replace access controls: internal DNS systems must also be protected from unauthorized clients.
5. Harden and update the DNS server
Keep DNS server software patched, remove unnecessary services, apply secure configuration baselines, and restrict administrative access to trusted systems.
6. Enable monitoring and periodic testing
Review DNS logs for unsuccessful and unexpected zone-transfer attempts. Retest the configuration after changes and verify that authorized secondary servers continue to receive legitimate updates.
3.4 Conclusion
The DNS assessment identifies an important information-disclosure vulnerability because the server allows an unauthorized AXFR request to succeed. Exposed records can assist attackers in mapping infrastructure, identifying possible targets, and preparing targeted phishing attempts.
The organization should immediately restrict zone transfers to authorized secondary servers, use TSIG authentication where appropriate, strengthen DNS firewall and access-control rules, separate internal and external DNS information, and monitor zone-transfer activity.
Conclusion: Proper DNS configuration and access control are essential for protecting network information. Correcting the AXFR misconfiguration reduces unnecessary information exposure and makes subsequent reconnaissance more difficult.
References for Technical Documentation
The following authoritative resources support the technical recommendations in these answers.
Nmap Project, Port Scanning Basics. Read Nmap documentation⁠�.
Nmap Project, Service and Version Detection. Read Nmap documentation⁠�.
OWASP Foundation, SQL Injection Prevention Cheat Sheet. Read OWASP guidance⁠�.
Cybersecurity and Infrastructure Security Agency (CISA), #StopRansomware Guide. Read CISA guidance⁠�.
CISA, NSA, FBI and MS-ISAC, Phishing Guidance: Stopping the Attack Cycle at Phase One. Read phishing guidance⁠�.
BIND 9 Documentation, Configuration Reference — allow-transfer. Read BIND DNS documentation⁠�.






https://chatgpt.com/share/6ad99467-6ad0-83ec-ae66-0e6d9c71343b?ogimg=plain