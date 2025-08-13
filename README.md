# prohormonePro — Releases & Verification

[![Pages deploy status](https://github.com/prohormonePro/prohormonepro.github.io/actions/workflows/pages/pages-build-deployment/badge.svg?branch=main)](https://github.com/prohormonePro/prohormonepro.github.io/actions/workflows/pages/pages-build-deployment)

**Quick links**
- 🔐 Trust & Verification: https://trust.prohormonepro.com/
- 📦 Latest release: https://github.com/prohormonePro/prohormonepro.github.io/releases/latest

---

## What this is

This repo hosts the public **trust page** (signing key + how to verify) and the **signed release artifacts**.

- Public key (Ed25519, Base64): `y37W950LEdhVcubih/vLL2JsQHPAII55dOAdiTnHW7k=`
- KeyID (first 12 hex of `sha256(pubkey_bytes)`): `PROD-92e36ec21a1e`

If you ever see a different key claiming to be me, assume it’s not legit.

---

## Verify a download (TL;DR)

You’re checking two things:
1) **Signature** → really came from me  
2) **Checksum** → not corrupted in transit

### 1) Signature (recommended)

- Download a file *and* its matching `.sig` from the latest release.
- Place the two archive `.sig` files inside: `Public_release/attestations/v1-prod/`
- Put the archive(s) **next to** the extracted `Public_release/` folder.

**Run verifiers (PowerShell, using any Python 3):**
```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -q pynacl
.\.venv\Scripts\python.exe .\Public_release\verify_exact.py
.\.venv\Scripts\python.exe .\Public_release\verify_packages.py
```

Expected:

```
VERIFY OK: spine_proof_manifest_fresh_.csv
VERIFY OK: SHA256SUMS.txt
VERIFY OK: Public_release.zip
VERIFY OK: Public_release.tar.gz
```

### 2) Checksums (optional)

Compare against the values in `Public_release/PACKAGES_CHECKSUMS.txt`.

**Windows (PowerShell):**

```powershell
Get-FileHash -Algorithm SHA256 .\Public_release.zip
Get-FileHash -Algorithm SHA256 .\Public_release.tar.gz
```

**macOS / Linux:**

```bash
shasum -a 256 Public_release.zip
shasum -a 256 Public_release.tar.gz
```

---

## Why signatures?

Signatures prove “this file came from the same key I’ve published” and that it hasn’t been altered.
They don’t prove who I am IRL; they prove continuity—**the same key keeps signing my releases**.

Cross-check the key here and on the trust page: [https://trust.prohormonepro.com/](https://trust.prohormonepro.com/)

---

## License

MIT — see [`LICENSE`](./LICENSE).
