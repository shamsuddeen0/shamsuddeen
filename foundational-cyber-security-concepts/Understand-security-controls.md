# 🛡️ Understanding Security Controls

**"Security is not just firewalls; it's also the door lock and the employee handbook."**

When I first started learning, I thought cybersecurity was 100% technical (Technical Controls). I quickly learned that you can have the best firewall in the world, but if the server room door is unlocked (Physical Control), or if an employee writes their password on a sticky note (Administrative Control), the firewall is useless.

Here is how I break down the "Defense in Depth" strategy.

---

## 🏗️ The 3 Pillars of Defense
I like to visualize security as protecting a **Castle**. You need rules, walls, and guards.

| Type | The Analogy | Real World Examples |
| :--- | :--- | :--- |
| **1. Administrative** | **"The Laws of the Kingdom"** <br> These are the policies and rules that tell people how to behave. | • Background checks<br>• Acceptable Use Policy (AUP)<br>• Mandatory training<br>• Separation of Duties |
| **2. Physical** | **"The Stone Walls & Moat"** <br> Stopping people from physically touching the hardware. | • Biometric locks<br>• Security guards<br>• CCTV Cameras<br>• Fences & Bollards |
| **3. Technical** | **"The Magic Forcefield"** <br> The software and hardware settings that stop digital attacks. | • Firewalls & IPS<br>• Encryption (AES/TLS)<br>• Antivirus (EDR)<br>• ACLs (Access Control Lists) |

---

## ⏱️ Controls by Function (The Timeline)
It is also important to classify controls by *when* they act during an attack.

### 🛑 1. Preventive (Before)
*Goal: Stop the attack from happening.*
*   **Physical:** A high fence.
*   **Technical:** A firewall dropping traffic.
*   **Admin:** Hiring employees who pass a background check.

### 🚨 2. Detective (During)
*Goal: Notice that an attack is happening.*
*   **Physical:** A motion sensor alarm.
*   **Technical:** An IDS (Intrusion Detection System) or SIEM logs.
*   **Admin:** A yearly security audit.

### 🩹 3. Corrective (After)
*Goal: Fix the mess after the attack.*
*   **Physical:** A fire extinguisher putting out a fire.
*   **Technical:** Restoring data from Backups.
*   **Admin:** The Incident Response Plan (IRP).

---

## 🧠 Other Important Concepts

### ⚠️ Deterrent Controls
These don't physically stop anyone, but they make the attacker think twice.
*   *Example:* A sign that says "Video Surveillance in Progress." (Even if the camera is broken, the sign works as a deterrent).

### 🔄 Compensating Controls
These are "Plan B" controls used when the primary control isn't possible.
*   *Example:* I cannot encrypt a legacy database (too old), so I isolate it on its own VLAN and put strict monitoring on it instead.

---

## 💡 Why This Matters?
If you are studying for **CompTIA Security+** or **CISSP**, this is guaranteed to be on the exam. 

But practically? As a pentester, I need to look for **gaps** in all three layers.
1.  Can I walk into the building? (Physical Fail)
2.  Can I social engineer the receptionist? (Administrative Fail)
3.  Can I bypass the firewall? (Technical Fail)

---

## 📚 Resources
*   [NIST SP 800-53](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final): The "Bible" of security controls.
*   [CIS Controls](https://www.cisecurity.org/controls): The top 18 critical security controls prioritized.