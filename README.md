# Apply OS hardening techniques
**Scenario**

Review the scenario below. Then complete the step-by-step instructions.

You are a cybersecurity analyst for yummyrecipesforme.com, a website that sells recipes and cookbooks. A former employee has decided to lure users to a fake website with malware. 

The former employee/ hacker executed a brute force attack to gain access to the web host. They repeatedly entered several known default passwords for the administrative account until they correctly guessed the right one. After they obtained the login credentials, they were able to access the admin panel and change the website’s source code. They embedded a javascript function in the source code that prompted visitors to download and run a file upon visiting the website. After embedding the malware, the hacker changed the password to the administrative account. When customers download the file, they are redirected to a fake version of the website that contains the malware. 

Several hours after the attack, multiple customers emailed yummyrecipesforme’s helpdesk. They complained that the company’s website had prompted them to download a file to access free recipes. The customers claimed that, after running the file, the address of the website changed and their personal computers began running more slowly. 

In response to this incident, the website owner tries to log in to the admin panel but is unable to, so they reach out to the website hosting provider. You and other cybersecurity analysts are tasked with investigating this security event.

To address the incident, you create a sandbox environment to observe the suspicious website behavior. You run the network protocol analyzer tcpdump, then type in the URL for the website, yummyrecipesforme.com. As soon as the website loads, you are prompted to download an executable file to update your browser. You accept the download and allow the file to run. You then observe that your browser redirects you to a different URL, greatrecipesforme.com, which contains the malware.  

The logs show the following process:

The browser initiates a DNS request: It requests the IP address of the yummyrecipesforme.com URL from the DNS server.

The DNS replies with the correct IP address. 

The browser initiates an HTTP request: It requests the yummyrecipesforme.com webpage using the IP address sent by the DNS server.

The browser initiates the download of the malware.

The browser initiates a DNS request for greatrecipesforme.com.

The DNS server responds with the IP address for greatrecipesforme.com.

The browser initiates an HTTP request to the IP address for greatrecipesforme.com.

A senior analyst confirms that the website was compromised. The analyst checks the source code for the website. They notice that javascript code had been added to prompt website visitors to download an executable file. Analysis of the downloaded file found a script that redirects the visitors’ browsers from yummyrecipesforme.com to greatrecipesforme.com. 

The cybersecurity team reports that the web server was impacted by a brute force attack. The disgruntled hacker was able to guess the password easily because the admin password was still set to the default password. Additionally, there were no controls in place to prevent a brute force attack. 

Your job is to document the incident in detail, including identifying the network protocols used to establish the connection between the user and the website.  You should also recommend a security action to take to prevent brute force attacks in the future.


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


