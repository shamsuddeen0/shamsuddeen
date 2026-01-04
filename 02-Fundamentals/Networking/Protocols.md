# 🌐 Common Network Protocols Explained

**"The language of the internet."**

As a hacker, I need to know these protocols better than the sysadmin who configured them. If I understand how they work, I understand how to break them.

---

## 📦 TCP vs. UDP (The Transport Layer)

### TCP (Transmission Control Protocol)
**"The Reliable One."**
*   **How it works:** It guarantees delivery. If a packet is lost, it is resent.
*   **The 3-Way Handshake:**
    1.  **SYN:** Client says "Hello?"
    2.  **SYN-ACK:** Server says "Hello! I hear you."
    3.  **ACK:** Client says "Great, let's talk."
*   **Hacking Context:** Nmap's `SYN Scan` (`-sS`) only sends the first packet to see if the port is open, then leaves. This is stealthier than completing the full handshake.

### UDP (User Datagram Protocol)
**"The Fast One."**
*   **How it works:** "Fire and forget." It sends packets without checking if they arrived. Used for streaming and DNS.
*   **Hacking Context:** Harder to scan because closed UDP ports often don't send an error message back. Nmap `-sU` is slow for this reason.

---

## 🌍 Application Layer Protocols

### HTTP / HTTPS (Web)
*   **Ports:** 80 (HTTP), 443 (HTTPS)
*   **Concept:** Request/Response. I ask for a page (`GET /index.html`), server gives it to me.
*   **Attack Vector:** This is the biggest attack surface. SQL Injection, XSS, and RCE all happen here.
*   **Tools:** Burp Suite, Nikto, Curl.

### DNS (Domain Name System)
*   **Port:** 53 (UDP/TCP)
*   **Concept:** The phonebook. Translates `google.com` to `142.250.190.46`.
*   **Attack Vector:**
    *   **Zone Transfer:** Asking the server for *every* subdomain it knows.
    *   **DNS Exfiltration:** Smuggling stolen data out inside DNS queries (because firewalls rarely block DNS).

### SSH (Secure Shell)
*   **Port:** 22
*   **Concept:** Encrypted remote command line.
*   **Attack Vector:**
    *   **Brute Force:** Trying thousands of passwords (noisy).
    *   **Key Theft:** Stealing the `id_rsa` file from a user's home directory.

### SMB (Server Message Block)
*   **Port:** 445
*   **Concept:** Windows File Sharing.
*   **Attack Vector:**
    *   **Null Sessions:** Logging in with no username/password.
    *   **EternalBlue (MS17-010):** The famous exploit that gives instant SYSTEM access on older Windows machines.

### FTP (File Transfer Protocol)
*   **Port:** 21
*   **Concept:** Moving files.
*   **Attack Vector:**
    *   **Anonymous Login:** Checking if user `anonymous` with password `anonymous` works.
    *   **Cleartext:** It sends passwords unencrypted. I can sniff them with Wireshark.

---

## 🧠 Protocol Cheat Sheet

| Protocol | Port | Transport | Description | Vulnerability |
| :--- | :--- | :--- | :--- | :--- |
| **FTP** | 21 | TCP | File Transfer | Cleartext Auth, Anonymous Login |
| **SSH** | 22 | TCP | Secure Shell | Weak Creds, Private Keys |
| **Telnet** | 23 | TCP | Remote Shell (Old) | Cleartext EVERYTHING |
| **SMTP** | 25 | TCP | Email Sending | User Enum, Open Relay |
| **DNS** | 53 | UDP | Domain Names | Zone Transfers |
| **HTTP** | 80 | TCP | Web (Unencrypted) | OWASP Top 10 |
| **POP3** | 110 | TCP | Email Retrieval | Cleartext |
| **SMB** | 445 | TCP | Windows Shares | EternalBlue, Null Session |
| **RDP** | 3389 | TCP | Remote Desktop | BlueKeep, Brute Force |