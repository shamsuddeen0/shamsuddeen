# 🕵️ Reconnaissance & OSINT

**"Information is currency."**

This directory covers the first phase of any engagement: **Passive Reconnaissance**. Before I send a single packet to the target server, I want to know everything about it using public sources.

## 📄 Contents
1.  **[OSINT-Workflow.md](OSINT-Workflow.md)**
    *   My step-by-step checklist for investigating a domain.
    *   From "Just a Company Name" to "List of Servers and Emails."

2.  **[Social-Engineering.md](Social-Engineering.md)**
    *   Tools for finding people, usernames, and emails (`Sherlock`, `theHarvester`).

3.  **[Asset-Discovery.md](Asset-Discovery.md)**
    *   Mapping the attack surface. Finding subdomains (`sub.target.com`) and cloud buckets.

---

## 🛑 Rules of Engagement
*   **Passive Only:** Everything in this folder interacts with *public* data (Google, Shodan, LinkedIn).
*   **No Scanning:** I do not run Nmap or Burp Suite in this phase.
*   **OpSec:** I always use a VPN and research accounts (sock puppets) to avoid alerting the target.