# ☀️ Management Wants a Word — TryHackMe CTF Walkthrough

<p align="center">
  <img src="docs/assets/banner.png" alt="Management Wants a Word TryHackMe Banner" width="100%">
</p>

<p align="center">
  <a href="https://tryhackme.com/">
    <img src="https://img.shields.io/badge/TryHackMe-Management%20Wants%20a%20Word-red?style=for-the-badge&logo=tryhackme" />
  </a>
  <img src="https://img.shields.io/badge/Difficulty-Hard-critical?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Platform-Windows-0078D4?style=for-the-badge&logo=windows&logoColor=white" />
  <img src="https://img.shields.io/badge/Focus-Forensics-blue?style=for-the-badge" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/DPAPI-Analysis-6f42c1?style=flat-square"/>
  <img src="https://img.shields.io/badge/Chrome-Credential%20Recovery-critical?style=flat-square"/>
  <img src="https://img.shields.io/badge/VeraCrypt-Container%20Analysis-success?style=flat-square"/>
  <img src="https://img.shields.io/badge/Documentation-Portfolio%20Project-0A66C2?style=flat-square"/>
</p>

---

## 📌 Overview

**Management Wants a Word** is a Hard TryHackMe forensics room built around a Windows triage image associated with a user named **Vera**.

This repository documents the evidence-driven investigation described in the supplied challenge material: offline Windows credential material is analyzed, a DPAPI-protected browser encryption key is recovered, Chrome's stored login database is decrypted, and the recovered password is used to access a VeraCrypt container containing the final challenge artifact.

The repository is intentionally written as a **professional forensic case study** rather than a direct answer sheet.

> **Purpose:** Demonstrate Windows forensic triage, registry-hive analysis, DPAPI concepts, browser credential analysis, encrypted-container investigation, evidence correlation, and security reporting inside an authorized TryHackMe laboratory.

---

# 🎯 Objectives

This walkthrough demonstrates how to:

* Analyze a Windows KAPE-style triage directory.
* Identify the SAM and SYSTEM registry hives.
* Explain offline extraction of a local account NT hash.
* Trace the Windows DPAPI protection chain.
* Recover the Chrome encryption key from `Local State`.
* Analyze the Chrome `Login Data` SQLite database.
* Recover the browser-stored password described by the challenge.
* Use that password to access the associated VeraCrypt container.
* Correlate the recovered artifacts into a single forensic conclusion.

---

# 🧠 Skills Demonstrated

| Domain | Techniques |
| --- | --- |
| **Digital Forensics** | Windows triage analysis, registry-hive analysis, artifact correlation |
| **Windows Internals** | SAM/SYSTEM, DPAPI |
| **Credential Analysis** | Offline account-hash recovery, browser credential analysis |
| **Browser Forensics** | Chrome `Local State`, `Login Data`, SQLite |
| **Cryptography** | DPAPI key protection, Chrome AES-GCM key hierarchy |
| **Encrypted Storage** | VeraCrypt container investigation |
| **Reporting** | Evidence-driven analysis, security impact, remediation |

---

# ⚙️ Lab Information

| Property | Value |
| --- | --- |
| Platform | TryHackMe |
| Room | Management Wants a Word |
| Room URL | https://tryhackme.com/room/hh-managementwantsaword-6bf3cc41 |
| Operating System | Windows |
| Difficulty | Hard |
| Category | Forensics |
| Environment | Authorized Lab |

---

# 🛠️ Tools & Artifacts Referenced

| Tool / Artifact | Purpose |
| --- | --- |
| **KAPE triage output** | Source evidence structure |
| **SAM / SYSTEM hives** | Offline Windows credential analysis |
| **Impacket `secretsdump.py`** | Offline SAM/SYSTEM extraction methodology |
| **DPAPI artifacts** | Windows-protected secret recovery |
| **Chrome `Local State`** | Browser encryption-key metadata |
| **Chrome `Login Data`** | Stored-login SQLite database |
| **SQLite tooling** | Browser database inspection |
| **DonPAPI / forensic scripts** | DPAPI analysis methodology referenced by the source material |
| **VeraCrypt** | Encrypted-container access |

> The source material references multiple possible forensic tools. This repository does not claim that an unverified tool or command was executed unless the source material explicitly supports it.

---

# 🔍 Investigation Methodology

The investigation follows the artifact-dependency chain presented by the challenge:

```text
Windows Triage Image
        │
        ▼
SAM + SYSTEM Registry Hives
        │
        ▼
Local Account NT Hash
        │
        ▼
User DPAPI Master Key
        │
        ▼
Chrome Local State
        │
        ▼
Chrome AES Encryption Key
        │
        ▼
Chrome Login Data
        │
        ▼
Recovered Browser Password
        │
        ▼
VeraCrypt Container
        │
        ▼
Final Challenge Artifact
```

The important forensic principle is **correlation**: no single artifact provides the complete answer. Each stage supplies material required to interpret the next.

---

# 🗂️ Repository Structure

```text
Management-Wants-a-Word-TryHackMe-Walkthrough/
│
├── README.md
├── _config.yml
│
├── Documentation/
│   └── THM_Management_Wants_a_Word_Documentation.md
│
├── Resources/
│   ├── notes.md
│   ├── payloads.md
│   ├── tools.md
│   ├── references.md
│   └── remediation.md
│
├── Screenshots/
│   ├── figure-1-room-overview.png
│   ├── figure-2-final-artifact-redacted.png
│   └── figure-3-sunrise-storyline.png
│
├── docs/
│   ├── index.md
│   └── assets/
│       ├── banner.png
│       ├── figure-1-room-overview.png
│       ├── figure-2-final-artifact-redacted.png
│       ├── figure-3-sunrise-storyline.png
│       └── css/
│           └── custom.scss
│
└── .github/
    └── workflows/
        └── pages.yml
```

---

# 🧩 Investigation Chain Summary

```text
Evidence Acquisition
        │
        ▼
Windows Triage Review
        │
        ▼
SAM / SYSTEM Identification
        │
        ▼
NT Hash Recovery
        │
        ▼
DPAPI Master-Key Analysis
        │
        ▼
Chrome Key Recovery
        │
        ▼
Chrome Credential Database Analysis
        │
        ▼
Password Correlation
        │
        ▼
VeraCrypt Container Access
        │
        ▼
Final Artifact
```

This is a **forensic artifact chain**, not a network exploitation chain. There is no unsupported claim of live initial access, lateral movement, or privilege escalation.

---

# 🔐 Flag Policy

To preserve the educational integrity of the TryHackMe room and discourage plagiarism, the actual challenge flag is **intentionally redacted**.

```text
[FLAG REDACTED]
```

The supplied final-artifact screenshot has also been sanitized so that only the flag value is removed while the surrounding invoice evidence remains visible.

---

# 📖 Documentation

The complete technical investigation is available in:

**[`Documentation/THM_Management_Wants_a_Word_Documentation.md`](Documentation/THM_Management_Wants_a_Word_Documentation.md)**

Supporting material is organized under **`Resources/`**, while evidence screenshots are stored in **`Screenshots/`** and duplicated under **`docs/assets/`** for GitHub Pages.

---

# 🖼️ Evidence

| Figure | Description |
| --- | --- |
| Figure 1 | TryHackMe room overview and challenge metadata |
| Figure 2 | Final artifact evidence with the challenge flag redacted |
| Figure 3 | Supplied Act 4 — Sunrise storyline illustration |

The repository contains only supplied evidence and a sanitized derivative of the supplied final-artifact image. No fake terminal output or fabricated forensic screenshot has been created.

---

# 🛡️ Security Findings

The investigation highlights several security-relevant conditions:

| Finding | Security Significance |
| --- | --- |
| Offline SAM/SYSTEM access | Enables local-account credential analysis when protected hives are obtained |
| DPAPI dependency on user credential material | Compromise of the relevant credential chain can expose protected secrets |
| Browser-saved credentials | Stored secrets can become recoverable during endpoint forensic analysis |
| Reusable password recovered from browser storage | Password reuse can bridge independent security boundaries |
| Encrypted container protected by recoverable password | Container security is weakened when the unlock secret is exposed elsewhere |

These are presented as **security observations from the lab evidence**, not as unsupported production vulnerability ratings.

---

# 📚 Key Learning Outcomes

After completing the investigation, the following practical skills are reinforced:

* Windows forensic triage.
* Offline registry-hive analysis.
* SAM/SYSTEM credential relationships.
* DPAPI artifact correlation.
* Chrome credential-storage architecture.
* SQLite database analysis.
* Encrypted-container investigation.
* Evidence-driven security reporting.

---

# 🔐 Defensive Perspective

A defensible endpoint configuration should reduce the chance that one compromised artifact can unlock another.

Recommended controls include:

* Protect offline access to Windows credential hives.
* Use strong account credentials and avoid password reuse.
* Minimize stored browser credentials on sensitive systems.
* Protect DPAPI recovery material and user profiles.
* Apply endpoint disk encryption and secure key management.
* Monitor unusual access to browser credential databases.
* Maintain least-privilege access to forensic and administrative tooling.
* Treat encrypted-container passwords as independent secrets.

---

# 🌐 GitHub Pages

A GitHub Pages site is included using the same Jekyll-based documentation model as the portfolio's reference repository.

The public documentation contains:

* Executive Summary
* Investigation Methodology
* Artifact Analysis
* Credential Recovery Chain
* Browser Forensics
* VeraCrypt Analysis
* Security Findings
* Defensive Recommendations
* Lessons Learned
* Conclusion

---

# ⚠️ Disclaimer

This repository documents analysis performed within an **authorized TryHackMe laboratory**.

The material is provided exclusively for:

* Cybersecurity education.
* Digital forensics learning.
* Capture The Flag documentation.
* Authorized security research.

Do not apply the techniques described here to systems or data without explicit authorization.

---

# 👨‍💻 Author

## **Anurag Revankar**

Cybersecurity Enthusiast • Penetration Testing • SOC • Digital Forensics

* Windows Security
* Digital Forensics
* Capture The Flag (CTF) Writeups
* TryHackMe Documentation
* Security Research

---

<p align="center">
  ⭐ If this documentation helps you understand Windows artifact analysis or forensic reporting methodology, consider starring the repository.
</p>
