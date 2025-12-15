# 🔑 Access Control Models (DAC, MAC, RBAC, ABAC)

**"Who is allowed to touch what?"**

Understanding Access Control is fundamental. It defines how a system decides if `User A` is allowed to read `File B`. Here is how I break down the four main types using real-world analogies.

---

## 1. DAC: Discretionary Access Control
**"The Owner is King."**

*   **The Concept:** The person who creates the file (the owner) decides who gets to see it. It is up to their "discretion."
*   **The Analogy:** **A House Party.** It's my house. I decide who comes in. I can let my best friend in, and I can kick my neighbor out. The police (Admin) don't decide; I do.
*   **Where I see it:**
    *   **Windows/Linux File Systems:** Right-clicking a folder and checking "Read Only" or granting permission to a specific user.
    *   **Google Drive:** When I click "Share" and type in your email address.

## 2. MAC: Mandatory Access Control
**" The System is King."**

*   **The Concept:** The Operating System or Security Policy decides. The user has **no say**. Even if I created the file, I cannot give you permission to see it unless you have the right "Security Clearance."
*   **The Analogy:** **The Military.** Even if the General likes me, he cannot show me a "Top Secret" document if I only have a "Confidential" badge. The rules are hard-coded into the system.
*   **Where I see it:**
    *   **SELinux / AppArmor:** Limiting what processes can do on a Linux server.
    *   Top Secret Government Systems.

## 3. RBAC: Role-Based Access Control
**"The Job Title is King."**

*   **The Concept:** Access is based on your **Job Function**, not your name. If you quit and a new person is hired, they get the same access instantly because they have the same role.
*   **The Analogy:** **A Hospital.**
    *   *Doctors* can write prescriptions.
    *   *Nurses* can view patient records.
    *   *Janitors* can open the supply closet.
    *   It doesn't matter *who* the Doctor is; the privileges belong to the "Doctor" badge.
*   **Where I see it:**
    *   **Corporate Environments:** "Sales Group," "HR Group," "IT Admins."
    *   **Azure / AWS IAM:** Assigning permissions to roles rather than individual users.

## 4. ABAC: Attribute-Based Access Control
**"The Context is King."**

*   **The Concept:** The most flexible and complex model. It looks at **Attributes** (Who, What, Where, When). It allows for "If/Then" logic.
*   **The Analogy:** **Buying Alcohol.**
    *   The store checks an attribute (Age > 21).
    *   It doesn't matter if you are a Doctor or a General (Role).
    *   It doesn't matter if the owner likes you (DAC).
    *   It strictly checks the specific data point (Attribute) of your ID.
*   **Where I see it:**
    *   **Firewalls:** "Allow access IF user is in HR AND IP address is inside the office AND time is 9am-5pm."
    *   **Zero Trust Architecture:** Dynamic access based on risk levels.

---

## ⚔️ Comparison Cheat Sheet

| Feature | DAC (Discretionary) | MAC (Mandatory) | RBAC (Role-Based) | ABAC (Attribute-Based) |
| :--- | :--- | :--- | :--- | :--- |
| **Who Decides?** | The Data Owner | The System / Policy | The Job Title | The Context / Rules |
| **Flexibility** | High (Easy to share) | Very Low (Rigid) | Medium (Corporate standard) | Highest (Granular) |
| **Complexity** | Low | High | Medium | High |
| **Best Use Case** | Personal PCs, File Sharing | Military, High Security | Companies, HR Systems | Cloud, Dynamic Environments |

---

## 🧠 My Takeaway
*   **RBAC** is what I will use 90% of the time in a corporate job.
*   **DAC** is what I use on my laptop.
*   **MAC** is for hardened systems (like NSA stuff).
*   **ABAC** is the future of cloud security.