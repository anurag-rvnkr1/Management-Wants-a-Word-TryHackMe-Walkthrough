# 🔐 Management Wants a Word — Payloads & Forensic Inputs

This room is a **forensics** challenge. It does not require a network exploit payload in the supplied source material.

## Artifact Inputs

The important investigation inputs are:

```text
SAM
SYSTEM
DPAPI master-key material
Chrome Local State
Chrome Login Data
VeraCrypt container
```

## Credential-Recovery Workflow

The source material describes an offline credential-analysis workflow:

```text
SAM + SYSTEM
      ↓
NT hash
      ↓
DPAPI master key
      ↓
Chrome AES key
      ↓
Encrypted Chrome password
      ↓
Plaintext credential
```

## Container Workflow

```text
Recovered Chrome password
      ↓
VeraCrypt container
      ↓
Mounted forensic volume
      ↓
Final artifact
```

## Handling Rule

Do not add real-world credentials, private keys, or unrelated secrets to this repository. Challenge-specific secrets are intentionally redacted from public documentation.
