
# Defensive Security
In the previous room, we learned about [offensive security](https://tryhackme.com/r/room/introtooffensivesecurity), which aims to identify and exploit system vulnerabilities to enhance security measures. This includes exploiting software bugs, leveraging insecure setups, and taking advantage of unenforced access control policies, among other strategies. Red teams and penetration testers specialize in these offensive techniques.

In this room, we will examine its counterpart, defensive security. It is concerned with two main tasks:

1. Preventing intrusions from occurring
2. Detecting intrusions when they occur and responding properly

<span style="color:rgb(255, 192, 0)">Blue teams</span> are part of the defensive security landscape.

Some of the tasks that are related tQo defensive security include:

- <span style="color:rgb(255, 192, 0)">User cyber security awareness</span>: Training users about cyber security helps protect against attacks targeting their systems.
- <span style="color:rgb(255, 192, 0)">Documenting and managing assets</span>: We need to know the systems and devices we must manage and protect adequately.
- <span style="color:rgb(255, 192, 0)">Updating and patching systems:</span> Ensuring that computers, servers, and network devices are correctly updated and patched against any known vulnerability (weakness).
- <span style="color:rgb(255, 192, 0)">Setting up preventative security devices:</span> firewall and intrusion prevention systems (IPS) are critical components of preventative security. Firewalls control what network traffic can go inside and what can leave the system or network. IPS blocks any network traffic that matches present rules and attack signatures.
- <span style="color:rgb(255, 192, 0)">Setting up logging and monitoring devices</span>: Proper network logging and monitoring are essential for detecting malicious activities and intrusions. If a new unauthorized device appears on our network, we should be able to detect it.

There is much more to defensive security. Aside from the above, we will also cover the following related topics:

- Security Operations Center (SOC)
- Threat Intelligence
- Digital Forensics and Incident Response (DFIR)
- Malware Analysis
# Search Skills

You are familiar with Internet search engines; however, how much are you familiar with specialized search engines? By that, we refer to search engines used to find specific types of results.

## Shodan

Let’s start with [Shodan](https://www.shodan.io/), a search engine for devices connected to the Internet. It allows you to search for specific types and versions of servers, networking equipment, industrial control systems, and IoT devices. You may want to see how many servers are still running Apache 2.4.1 and the distribution across countries. To find the answer, we can search for `apache 2.4.1`, which will return the list of servers with the string “apache 2.4.1” in their headers.
Consider visiting Shodan [Search Query Examples](https://www.shodan.io/search/examples) for more examples. Furthermore, you can check [Shodan trends](https://trends.shodan.io/) for historical insights if you have a subscription.
## Censys

At first glance, [Censys](https://search.censys.io/) appears similar to Shodan. However, Shodan focuses on Internet-connected devices and systems, such as servers, routers, webcams, and IoT devices. Censys, on the other hand, focuses on Internet-connected hosts, websites, certificates, and other Internet assets. Some of its use cases include enumerating domains in use, auditing open ports and services, and discovering rogue assets within a network. You might want to check [Censys Search Use Cases](https://support.censys.io/hc/en-us/articles/20720064229140-Censys-Search-Use-Cases).

## VirusTotal

[VirusTotal](https://www.virustotal.com/) is an online website that provides a virus-scanning service for files using multiple antivirus engines. It allows users to upload files or provide URLs to scan them against numerous antivirus engines and website scanners in a single operation. They can even input file hashes to check the results of previously uploaded files.

## Have I Been Pwn
ed

[Have I Been Pwned](https://haveibeenpwned.com/) (HIBP) does one thing; it tells you if an email address has appeared in a leaked data breach. Finding one’s email within leaked data indicates leaked private information and, more importantly, passwords. Many users use the same password across multiple platforms

## CVE
We can think of the<span style="color:rgb(255, 192, 0)"> Common Vulnerabilities and Exposures (CVE) </span>program as a <span style="color:rgb(255, 192, 0)">dictionary</span> of vulnerabilities. It provides a <span style="color:rgb(255, 192, 0)">standardized identifier</span> for vulnerabilities and security issues in software and hardware products. Each vulnerability is assigned a <span style="color:rgb(0, 176, 80)">CVE ID</span> with a standardized format like `CVE-2024-29988`.<span style="color:rgb(0, 176, 80)"> This unique identifier (CVE ID)</span> ensures that everyone from security researchers to vendors and IT professionals is referring to the same vulnerability, [CVE-2024-29988](https://nvd.nist.gov/vuln/detail/CVE-2024-29988) in this case.

The MITRE Corporation maintains the CVE system. For more information and to search for existing CVEs, visit the [CVE Program](https://www.cve.org/) website. Alternatively, visit the [National Vulnerability Database](https://nvd.nist.gov/) (NVD) website. The screenshot below shows CVE-2014-0160, also known as Heartbleed.

## Exploit Database
Now that we have permission to exploit a vulnerable system, we might need to find a working exploit code. One resource is the [Exploit Database](https://www.exploit-db.com/). The Exploit Database lists exploit codes from various authors; some of these <span style="color:rgb(0, 176, 80)">exploit codes are tested and marked as verified.</span>
![[TryHackMe-20241122202415054.webp]]


## Linux Manual Pages
Let’s say we want to check the manual page for the command `ip`. We issue the command `man ip`. The screenshot below shows the page we received. You might want to start the AttackBox and run `man ip` on the terminal. Press `q` to quit.

## Microsoft Windows
Microsoft provides an official [Technical Documentation](https://learn.microsoft.com/) page for its products.