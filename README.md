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
