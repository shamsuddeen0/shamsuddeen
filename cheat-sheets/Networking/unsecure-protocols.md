# 🚫 Insecure Protocols & Services

**"The ghosts of the internet's past."**

Many protocols designed in the 80s and 90s were built for trust, not security. They send passwords in cleartext or have massive vulnerabilities.

As a pentester, finding these on a network is like finding a pot of gold. As a defender, you must kill them immediately.

---

## 🔌 Remote Access (The "Cleartext" Offenders)
*These protocols send your username and password in plain text. Anyone with Wireshark can steal them.*

| Insecure Protocol | Why it's bad | Secure Replacement |
| :--- | :--- | :--- |
| **Telnet** (Port 23) | Sends keystrokes in cleartext. | **SSH** (Secure Shell) |
| **Rlogin** | "Remote Login." Trust-based authentication (no password required if IP is trusted). | **SSH** |
| **Rsh** | "Remote Shell." Similar to Rlogin, executes commands without encryption. | **SSH** |
| **Finger** | Reveals user info (full name, login time, home directory). Huge privacy leak. | **None** (Just disable it) |

---

## 📂 File Sharing & Directory Services
*Services that often expose too much information or allow unauthorized access.*

| Insecure Service | Why it's bad | Mitigation / Replacement |
| :--- | :--- | :--- |
| **FTP** (Port 21) | Cleartext credentials. Vulnerable to sniffing. | **SFTP** or **FTPS** |
| **TFTP** (Port 69) | Trivial FTP. No authentication at all. Anyone can read/write if they know the filename. | Disable unless strictly needed (e.g., PXE Boot). |
| **NFS** (Network File System) | Often configured with "no_root_squash" (Privilege Escalation risk) or IP-only auth. | Use strict ACLs or **SMBv3** (Signed). |
| **SMBv1** | The protocol behind the **WannaCry** ransomware (EternalBlue exploit). | **SMBv2 / SMBv3** (Disable v1 immediately!) |
| **NIS** (ypbind/ypserv) | "Yellow Pages." Sends map data (passwords/users) unencrypted. | **LDAP** (over SSL) or **Kerberos**. |

---

## 📧 Email & Communication
*Old mail protocols are spam and spoofing magnets.*

| Insecure Service | Why it's bad | Secure Replacement |
| :--- | :--- | :--- |
| **POP3** (Port 110) | Downloads email in cleartext. | **POP3S** (SSL/TLS) |
| **IMAP** (Port 143) | Reads email in cleartext. | **IMAPS** (SSL/TLS) |
| **SMTP** (Port 25) | Sends email. Open relays allow spammers to use your server. | **SMTPS** (Port 465/587) + Authentication. |
| **Sendmail** | An ancient mail daemon notorious for buffer overflows and root exploits in older versions. | **Postfix** or **Exim** (Configured securely). |

---

## 🛠️ Miscellaneous Dangerous Services
*If you see these open, investigate immediately.*

*   **Authd / Identd (Port 113):** Reveals the owner of a TCP connection. Helps attackers map users to processes.
*   **Rwhod:** Broadcasts who is logged in on the local network. Information Disclosure.
*   **Netdump:** Sends crash dumps over the network unencrypted. Can leak sensitive memory data (passwords, keys).
*   **SNMPv1 / SNMPv2c:** Network management. Uses "Community Strings" (passwords) sent in cleartext. Attackers can map your entire network topology. (Use **SNMPv3**).

---

## 🧠 Defender's Checklist
1.  **Scan:** Run `nmap -sV` to find versions.
2.  **Verify:** Check if SSL/TLS is wrapped around the service.
3.  **Kill:** If Telnet or Rsh is running, shut it down. There is zero excuse for using them in 2024.