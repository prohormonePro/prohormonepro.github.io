---
title: ProhormonePro — Trust & Verification
description: Signed releases and how to verify them. Just so you know it's me.
---

*Just so you know it's me.*

## Public key

**Ed25519 (Base64)**  
`y37W950LEdhVcubih/vLL2JsQHPAII55dOAdiTnHW7k=`

**KeyID** (first 12 hex of sha256(pubkey bytes))  
`PROD-92e36ec21a1e`

> If you ever see a different key claiming to be me, assume it's not legit.

---

## Latest release

Artifacts ship with detached signatures:

- `Public_release.zip` + `Public_release.zip.sig`  
- `Public_release.tar.gz` + `Public_release.tar.gz.sig`

---

## How to verify (quick)

You’re checking two things:  
1) **Signature** = came from me  
2) **Checksum** = not corrupted

### A) Signature (recommended)

1. Put the archive(s) and the extracted `Public_release/` folder **side-by-side**.

   ```text
   Downloads/
   ├─ Public_release.zip
   ├─ Public_release.tar.gz
   └─ Public_release/
      ├─ spine_proof_manifest_fresh_.csv
      ├─ SHA256SUMS.txt
      ├─ VERIFY_README.txt
      ├─ verify_exact.py
      ├─ verify_packages.py
      ├─ footprint/                 (optional)
      │  └─ SHA256SUMS_sand.txt     (optional)
      └─ attestations/
         └─ v1-prod/
            ├─ public_key_base64.txt
            ├─ spine_proof_manifest_fresh_.csv.sig
            ├─ SHA256SUMS.txt.sig
            ├─ SHA256SUMS_sand.txt.sig   (if present)
            ├─ Public_release.zip.sig
            └─ Public_release.tar.gz.sig
   ```

2. Create a temporary Python env and install PyNaCl:

   ```powershell
   python -m venv .venv
   .\.venv\Scripts\python.exe -m pip install -q pynacl
   ```

3. Run the included verifiers:

   ```powershell
   .\.venv\Scripts\python.exe .\Public_release\verify_exact.py
   .\.venv\Scripts\python.exe .\Public_release\verify_packages.py
   ```

**Expected output:**

```text
VERIFY OK: spine_proof_manifest_fresh_.csv
VERIFY OK: SHA256SUMS.txt
VERIFY OK: Public_release.zip
VERIFY OK: Public_release.tar.gz
```

**Why this works**: I sign releases with my private key. Anyone can verify with the public key above. Any change to a file breaks the signature.

### B) Checksums (optional)

`Public_release/PACKAGES_CHECKSUMS.txt` lists SHA-256 and MD5 for both archives. Re-hash locally and compare:

**Windows (PowerShell)**

```powershell
Get-FileHash -Algorithm SHA256 .\Public_release.zip
Get-FileHash -Algorithm SHA256 .\Public_release.tar.gz
```

**macOS / Linux**

```bash
shasum -a 256 Public_release.zip
shasum -a 256 Public_release.tar.gz
```

**Plain-English**  
Signatures prove “this file really came from me and hasn’t been altered.”  
They don’t prove who I am IRL; they prove continuity: the same key keeps signing my releases. I’ll publish the same public key (and KeyID `PROD-92e36ec21a1e`) in multiple places so you can cross-check.

**Questions?**  
If something doesn’t verify or a step isn’t clear, contact me where you got the download link. I’d rather you pause and ask than run unverified code.
