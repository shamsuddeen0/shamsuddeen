# 🧰 My Recon Toolkit

**"I don't fear the man who has practiced 10,000 tools once. I fear the man who has practiced one tool 10,000 times."**

This is not a random dump of links. These are the tools you can actually use during CTFs and assessments, categorized by their function.

---

## 🌐 Subdomain & DNS Enumeration
*Finding the attack surface.*

| Tool | Why I Use It | Link |
| :--- | :--- | :--- |
| **Amass** | The industry standard. It scrapes valid subdomains from 50+ data sources. | [GitHub](https://github.com/owasp-amass/amass) |
| **Subfinder** | Extremely fast. I use this when I just need a quick list to pipe into other tools. | [GitHub](https://github.com/projectdiscovery/subfinder) |
| **Findomain** | Written in Rust, it uses Certificate Transparency logs to find subdomains instantly. | [GitHub](https://github.com/Findomain/Findomain) |
| **Smap** | A cool tool from my research: it acts like Nmap but fetches data passively from Shodan (no touching the target!). | [GitHub](https://github.com/s0md3v/Smap) |

## 🕸️ Content Discovery (Fuzzing)
*Finding hidden files and directories.*

| Tool | Why I Use It | Link |
| :--- | :--- | :--- |
| **Feroxbuster** | My favorite fuzzer. It's written in Rust, supports recursion, and is incredibly fast. | [GitHub](https://github.com/epi052/feroxbuster) |
| **FFUF** | "Fuzz Faster U Fool." The flexible standard for web fuzzing. | [GitHub](https://github.com/ffuf/ffuf) |
| **AutoRecon** | A lifesaver for CTFs. It runs Nmap, Nikto, and Gobuster automatically and organizes the output. | [GitHub](https://github.com/Tib3rius/AutoRecon) |

## 👤 OSINT & People
*Finding users, emails, and social footprints.*

| Tool | Why I Use It | Link |
| :--- | :--- | :--- |
| **Maigret** | The best tool for finding a username across thousands of sites (better than Sherlock). | [GitHub](https://github.com/soxoj/maigret) |
| **h8mail** | Checks if an email has been found in past data breaches. | [GitHub](https://github.com/khast3x/h8mail) |
| **GitRecon** | Scans GitHub profiles to find leaked email addresses in commits. | [GitHub](https://github.com/hidjn/GitRecon) |

## ☁️ Cloud & Infrastructure
*Scanning AWS, Azure, and Buckets.*

| Tool | Why I Use It | Link |
| :--- | :--- | :--- |
| **S3Enum** | Fast enumeration of Amazon S3 buckets (often full of sensitive data). | [GitHub](https://github.com/koenrh/s3enum) |
| **CloudUnflare** | attempts to find the *real* IP address behind a Cloudflare protected site. | [GitHub](https://github.com/greycatz/CloudUnflare) |

## 🏰 Active Directory
*Internal network mapping.*

| Tool | Why I Use It | Link |
| :--- | :--- | :--- |
| **Enum4Linux-ng** | The modern rewrite of the classic tool. Extracts users and shares from SMB. | [GitHub](https://github.com/cddmp/enum4linux-ng) |
| **ADReaper** | A newer tool specifically designed for fast AD enumeration. | [GitHub](https://github.com/0xJs/ADReaper) |

---

### 🗑️ The Graveyard (Deprecated/Niche)
*Tools I am aware of but rarely use, or that have been replaced.*
*   *Twint:* Was great for Twitter, but API changes broke it.
*   *Legion:* Good GUI, but I prefer command line tools for speed.
*   *Osmedeus:* A massive automated framework. Good, but too noisy for my learning path right now.