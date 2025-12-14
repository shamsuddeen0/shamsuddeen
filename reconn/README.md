# 🕵️ Active & Passive Reconnaissance

**"If you can't find it, you can't hack it."**

Reconnaissance is the most critical phase of the kill chain. If I don't know a server or a webpage exists, I can't test it. This page documents the tools and techniques I use to map out a target.

## 🧠 In a Nutshell: Active vs. Passive
Before using the tools, it is important to understand the difference. I like to use the "House Security" analogy:

| Feature | ☁️ Passive Recon | ⚡ Active Recon |
| :--- | :--- | :--- |
| **The Analogy** | **"The Stalker"** <br> You sit in a car across the street watching the house. You check the owner's social media to see if they are on vacation. | **"The Knocker"** <br> You walk up to the house and jiggle the handle to see if it's locked. You knock on the door to see who answers. |
| **Definition** | Gathering information from public sources *without* directly interacting with the target's servers. | Interacting directly with the target system by sending packets and requests. |
| **Stealth** | **100% Stealthy.** The target has no idea you are watching because you never touch their network. | **Noisy.** Your IP address will appear in their firewall logs and intrusion detection systems. |
| **Tools** | Google, Whois, Shodan, LinkedIn. | Nmap, Burp Suite, Nikto, Nuclei. |

---

## ☁️ Passive Recon Tools (OSINT)
*Gathering information without alerting the target.*

### 🔍 Search Engines & Dorks
*   **[Google Hacking Database (GHDB)](https://www.exploit-db.com/google-hacking-database)**: A collection of search queries to find exposed files, login portals, and errors.
*   **[Shodan](https://www.shodan.io/)**: The "Google" for IoT devices, servers, and webcams.
*   **[Censys](https://censys.io)**: Similar to Shodan, excellent for finding certificates and hosts.
*   **[Wayback Machine](https://archive.org/web/)**: I use this to find old versions of a site, which might contain removed comments or old backup files.

### 🌐 DNS & Subdomains
*   **[crt.sh](https://crt.sh/)**: Search for SSL/TLS certificates to find subdomains that aren't even active yet.
*   **[DNSDumpster](https://dnsdumpster.com/)**: Visualizes domain mapping and finds related hosts.
*   **[Amass](https://github.com/owasp-amass/amass)**: The industry standard for deep DNS enumeration.
*   **[Sublist3r](https://github.com/aboul3la/Sublist3r)**: A fast python tool to enumerate subdomains across multiple search engines.

### 👤 People & Social Media
*   **[Sherlock](https://github.com/sherlock-project/sherlock)**: I use this to hunt down a username across hundreds of social media sites instantly.
*   **[theHarvester](https://github.com/laramies/theHarvester)**: Gathers emails, names, subdomains, IPs, and URLs from public sources.
*   **[LinkedIn](https://www.linkedin.com)**: Essential for understanding the "Tech Stack" a company uses based on their job postings.

---

## ⚡ Active Recon Tools
*⚠️ **Warning:** These tools generate traffic and logs. Only use these on targets you have permission to test.*

### 🗺️ Network Scanning
*   **[Nmap](https://nmap.org/)**: The most important tool in this list.
    *   *My standard command:* `nmap -sC -sV -oA scan_results <IP>`
    *   *Reference:* See my [Nmap Cheat Sheet](../cheat-sheets/nmap.md).
*   **[RustScan](https://github.com/RustScan/RustScan)**: I use this when I need to scan ports extremely fast (faster than Nmap).

### 🕸️ Web Enumeration
*   **[Burp Suite](https://portswigger.net/burp)**: The #1 tool for web hacking. I use the Community Edition for manual testing.
*   **[FFUF](https://github.com/ffuf/ffuf)**: "Fuzz Faster U Fool" - My go-to tool for brute-forcing directories and files.
*   **[Wappalyzer](https://www.wappalyzer.com/)**: A browser extension that tells me what technologies a website is built with (CMS, Frameworks, etc).

### ☢️ Vulnerability Scanning
*   **[Nuclei](https://github.com/projectdiscovery/nuclei)**: A modern, template-based scanner. Highly effective for bug bounties.
*   **[OWASP ZAP](https://www.zaproxy.org)**: A great open-source alternative to Burp Suite.