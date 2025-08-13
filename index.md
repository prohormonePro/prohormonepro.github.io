# ProhormonePro — Trust & Verification

**Public key (Base64):** `y37W950LEdhVcubih/vLL2JsQHPAII55dOAdiTnHW7k=`  
**KeyID:** `PROD-92e36ec21a1e`

---

## Latest release (artifacts)
- `Public_release.zip` + `Public_release.zip.sig`  
  - SHA256: `6D241248F9F5397B0F7300C62C516ABBB74B4E6D1C0303DBF803E0DF2ED61831`  
  - MD5:    `108C0530247898E8BFB1F043B38D26D1`
- `Public_release.tar.gz` + `Public_release.tar.gz.sig`  
  - SHA256: `50B5654865F4B7603714B2E47665824C9EDF5B05BD0EEE4CBE2AB983608B8080`  
  - MD5:    `A966CD273ADD2DA787019B0A9D2C0CD7`

*(Hashes & KeyID are taken from the signed `RELEASE_SUMMARY.json` for this release.)*

---

## Verify (quick start)
1) **Download** a file *and* its matching `.sig`.  
2) **Check the key** above matches what you see in my other places (this page, GitHub README, etc.).  
3) **Run a verifier**:
   - If you downloaded the full `Public_release/` folder, use the included `verify_exact.py` (for contents) and `verify_packages.py` (for the two archives).
   - Or verify with any Ed25519/NaCl tool using the public key on this page.

### Windows quick check (PowerShell)
```powershell
# From the release folder:
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -q pynacl
.\.venv\Scripts\python.exe .\verify_exact.py      # verifies manifest + sums
.\.venv\Scripts\python.exe .\verify_packages.py   # verifies the .zip/.tar.gz against .sig
