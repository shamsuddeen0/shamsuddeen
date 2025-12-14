# 🧰 The Extended Tool Chest

**"A good hacker has a big toolbox, but knows exactly which one to pick."**

While you rely on the core tools (Nmap, Burp, Metasploit) for 90% of the work, these are specialized tools I have collected for specific scenarios.

---

## 🌐 Web Exploitation (Specific Attacks)
*When generic scanners fail, you can use these for targeted attacks.*

| Tool | Purpose |
| :--- | :--- |
| **[SQLMap](https://github.com/sqlmapproject/sqlmap)** | The King of SQL Injection. Automates detection and database takeover. |
| **[Commix](https://github.com/commixproject/commix)** | Automated All-in-One OS Command Injection tool. |
| **[WPScan](https://github.com/wpscanteam/wpscan)** | The standard for finding vulnerabilities in WordPress sites. |
| **[XSStrike](https://github.com/s0md3v/XSStrike)** | A smart XSS detection suite that generates payloads instead of just checking signatures. |
| **[Arjun](https://github.com/s0md3v/Arjun)** | Finds hidden HTTP parameters (e.g., `?debug=true`) that other scanners miss. |

---

## 📡 Wireless & Network Attacks
*Auditing WiFi and local networks.*

| Tool | Purpose |
| :--- | :--- |
| **[Airgeddon](https://github.com/v1s1t0r1sh3r/airgeddon)** | A multi-use bash script for Linux to audit wireless networks (Handshakes, Evil Twin, WEP/WPA). |
| **[WiFi-Pumpkin](https://github.com/P0cL4bs/WiFi-Pumpkin)** | Framework for creating Rogue Wi-Fi Access Points (Evil Twin attacks). |
| **[Bettercap](https://github.com/bettercap/bettercap)** | The "Swiss Army Knife" for network attacks (MITM, Sniffing, Spoofing). |
| **[Wifite2](https://github.com/derv82/wifite2)** | "Automated" wireless attack tool. Great for quick audits. |

---

## 📱 Mobile Hacking (Android/iOS)
*Analyzing apps for hardcoded secrets and vulnerabilities.*

| Tool | Purpose |
| :--- | :--- |
| **[MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF)** | Mobile Security Framework. Drop an APK in, get a full security report. |
| **[Frida](https://frida.re/)** | Dynamic instrumentation toolkit. Lets you inject scripts into native apps (Bypass SSL Pinning). |
| **[Objection](https://github.com/sensepost/objection)** | A runtime mobile exploration toolkit (uses Frida but easier). |
| **[Qark](https://github.com/linkedin/qark)** | LinkedIn's tool for finding security holes in Android apps. |

---

## 🧩 Reverse Engineering & Malware
*Taking things apart to see how they work.*

| Tool | Purpose |
| :--- | :--- |
| **[Ghidra](https://ghidra-sre.org/)** | The NSA's open-source reverse engineering suite. (Free alternative to IDA Pro). |
| **[Cutter](https://github.com/rizinorg/cutter)** | A graphical user interface for the Rizin/Radare2 framework. |
| **[dnSpy](https://github.com/dnSpy/dnSpy)** | The absolute best debugger and editor for .NET assemblies. |
| **[PeStudio](https://www.winitor.com/)** | Static analysis of Windows executables (finds suspicious imports/strings). |

---

## 💀 Post-Exploitation & C2
*What comes after you get a shell.*

| Tool | Purpose |
| :--- | :--- |
| **[Evil-WinRM](https://github.com/Hackplayers/evil-winrm)** | The ultimate shell for hacking Windows machines with WinRM enabled. |
| **[Mimikatz](https://github.com/gentilkiwi/mimikatz)** | Extracts plain-text passwords, hashes, and PIN codes from memory. |
| **[Covenant](https://github.com/cobbr/Covenant)** | A .NET Command and Control (C2) framework. |
| **[PoshC2](https://github.com/nettitude/PoshC2)** | A proxy-aware C2 framework used heavily for lateral movement. |

---

## ☁️ Cloud Security (AWS/Azure)
*Auditing modern infrastructure.*

| Tool | Purpose |
| :--- | :--- |
| **[ScoutSuite](https://github.com/nccgroup/ScoutSuite)** | Multi-cloud security auditing tool (AWS, Azure, GCP). |
| **[CloudSploit](https://github.com/aquasecurity/cloudsploit)** | Detects potential security risks in cloud accounts. |