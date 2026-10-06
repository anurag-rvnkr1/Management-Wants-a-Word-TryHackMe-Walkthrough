# ☀️ Management Wants a Word — Investigation Notes

## Challenge Profile

| Property | Value |
| --- | --- |
| Platform | TryHackMe |
| Room | Management Wants a Word |
| Difficulty | Hard |
| Category | Forensics |
| Operating System | Windows |
| Room URL | https://tryhackme.com/room/hh-managementwantsaword-6bf3cc41 |

---

## Primary Evidence Locations

```text
Users\Vera\
Windows\System32\config\
```

Important artifacts described by the challenge:

```text
SAM
SYSTEM
SECURITY
Users\Vera\AppData\Roaming\Microsoft\Protect\<SID>\
Users\Vera\AppData\Local\Google\Chrome\User Data\Local State
Users\Vera\AppData\Local\Google\Chrome\User Data\Default\Login Data
```

---

## Investigation Chain

```text
SAM + SYSTEM
      ↓
minivera NT hash
      ↓
DPAPI master key
      ↓
Chrome encrypted key
      ↓
Chrome AES key
      ↓
Login Data
      ↓
Recovered password
      ↓
VeraCrypt container
      ↓
Final artifact
```

---

## Evidence Boundaries

Only three supplied images were available for this repository package:

1. TryHackMe room overview.
2. Final invoice artifact containing the challenge flag.
3. Act 4 — Sunrise storyline illustration.

The second image has been sanitized so that the flag itself is not published.

No terminal screenshots for `secretsdump.py`, DPAPI recovery, Chrome database decryption, or container mounting were supplied. Those stages are therefore documented from the provided source material and are not represented as independently captured command evidence.

---

## Important Technical Relationships

### SAM + SYSTEM

The source material uses these hives for offline local-account credential analysis.

### DPAPI

The user credential material is used to recover the relevant DPAPI master key.

### Chrome

`Local State` contains the encrypted browser key material. `Login Data` contains encrypted login records.

### VeraCrypt

The recovered Chrome password is reused as the password for the VeraCrypt container in the challenge chain.

---

## Redaction Policy

The actual TryHackMe flag is intentionally excluded from:

* README.md
* Documentation
* GitHub Pages
* Captions
* Alt text
* Metadata
* Filenames
* Images

The sanitized final-artifact image preserves the invoice structure while replacing the flag with:

```text
[FLAG REDACTED]
```
