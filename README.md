# Security Incident Report: OS Hardening Techniques

## Scenario
You are a cybersecurity analyst for **yummyrecipesforme.com**, a website that sells recipes and cookbooks. A former employee executed a brute force attack to gain access to the web host by repeatedly entering several known default passwords for the administrative account until successful.

Once the attacker accessed the admin panel, they changed the website’s source code and embedded a JavaScript function prompting visitors to download and run a file. After embedding the malware, they changed the administrative password. Users who downloaded the file were redirected to a fake website, `greatrecipesforme.com`, which hosted malware.

Hours later, customers contacted support after their devices slowed down and redirected to a suspicious site.

---

## Section 1: Identify the Network Protocol Involved in the Incident

The network protocol involved in this incident is **Hypertext Transfer Protocol (HTTP)**.

Since the issue involves accessing the web server of yummyrecipesforme.com, HTTP traffic was used. Using `tcpdump` to monitor the interaction with the site confirmed that HTTP was used to load the web content and initiate the download of the malicious file. This confirms activity at the **application layer**, specifically involving HTTP.

---

## Section 2: Document the Incident

The incident was reported by customers attempting to access **yummyrecipesforme.com**, who reached out to the help desk after being prompted to download a suspicious file. After executing the file, users were redirected to another website and their systems became slow.

The web server owner attempted to access the admin panel but could no longer log in with their credentials.

A sandbox environment was created to investigate the incident safely. The cybersecurity analyst ran `tcpdump` to capture network traffic. When the website was accessed, the browser immediately prompted a file download. Once executed, the browser redirected to `greatrecipesforme.com`.

### Logs and Findings:
- The browser first initiated a DNS request for **yummyrecipesforme.com**.
- The DNS response returned the correct IP address.
- An HTTP request was made to the IP to access the website.
- A download was triggered for the malicious executable.
- A second DNS request was made for **greatrecipesforme.com**.
- A new IP address was received, and the browser was redirected.

The senior cybersecurity analyst escalated the investigation. On reviewing the website’s source code and analyzing the downloaded file, it was found that the attacker had injected a script prompting file download, which redirected users to a malicious clone site.

It was concluded that a **brute force attack** had occurred, allowing the attacker to log in using a **default password** and then change it, locking out the legitimate administrator.

---

## Section 3: Recommend One Remediation for Brute Force Attacks

To mitigate brute force attacks, it is recommended to **disallow the reuse of previous passwords**. Since the attacker exploited a default password to gain access, it’s essential to enforce controls that block the use of known or old passwords.

### Additional Recommendations:
- **Require frequent password changes** to limit the window of compromise in case of exposure.
- **Implement Two-Factor Authentication (2FA)** for administrative accounts to enforce a second layer of verification, such as an OTP sent via email or SMS.

These steps significantly reduce the likelihood of brute force attacks and unauthorized access to sensitive systems.

---

## Summary

This incident demonstrates the importance of **OS hardening**, secure password policies, and proactive monitoring. By enforcing stronger authentication and disabling default credentials, organizations can reduce attack surfaces and protect against similar breaches.

---


