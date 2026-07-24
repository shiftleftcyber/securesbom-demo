# 🧩 SecureSBOM Maven Showcase Demo

This repository demonstrates SecureSBOM in a real CI/CD workflow using a Maven project containing a **vulnerable Log4J 2.14.1 dependency**.  
It shows how SecureSBOM:
- Generates SBOMs using CycloneDX
- Signs and verifies SBOMs via `shiftleftcyber/secure-sbom-action`
- Demonstrates interoperability by signing SBOMs and SBOM digests with ReARM actions, then verifying them with SecureSBOM APIs
- Detects tampering (modifications post-signing)
- Enforces security gates before deployment
- Automatically signs SBOMs during GitHub releases
- Runs OSV vulnerability scans (source and SBOM)

## 🧱 Structure
- `demo-app/` — Maven project with Log4J 2.14.1
- `.github/workflows/secure-sbom-showcase-maven.yml` — Main CI/CD workflow
- `.github/workflows/demo-rearm-securesbom-interoperability.yml` — ReARM signing and SecureSBOM verification interoperability workflow
- `osv-report-template.html` — Dark terminal-themed SecureSBOM CI/CD report
- `README.md` — You are here 😎

## 🚀 Usage
1. Add repository secrets:
   - `SECURE_SBOM_API_KEY`
2. Add repository variables:
   - `SECURE_SBOM_SIGNING_KEY_ID`
   - `SECURE_SBOM_API_URL` (optional; workflows default to the production SecureSBOM API when unset)
3. GitHub automatically provides `GITHUB_TOKEN`.
4. Trigger the workflow manually under **Actions → SecureSBOM Showcase** or **Actions → SecureSBOM Demo - ReARM Interoperability**.
5. Watch the results:
   - Signed SBOM artifacts
   - ReARM-generated SBOMs signed in detached SBOM and digest modes
   - Verification pass/fail
   - OSV scan logs
   - Tamper detection
   - Pretty HTML report in summary or downloadable artifact

> **Note:** This demo intentionally includes a vulnerable dependency (Log4J 2.14.1) for educational purposes only. Do not deploy this code in production.

The ReARM interoperability workflow keeps the CycloneDX SBOM signature detached as the published artifact. For verification, it mirrors the SecureSBOM SDK CLI behavior: the workflow builds the v2 verify API request from the original CycloneDX SBOM plus the detached JSF signature object, without using `signature_b64`.
