# 🧩 SecureSBOM Maven Showcase Demo

This repository demonstrates SecureSBOM in a real CI/CD workflow using a Maven project containing a **vulnerable Log4J 2.14.1 dependency**.  
It shows how SecureSBOM:
- Generates SBOMs using CycloneDX
- Signs and verifies SBOMs via `shiftleftcyber/secure-sbom-action`
- Detects tampering (modifications post-signing)
- Enforces security gates before deployment
- Automatically signs SBOMs during GitHub releases
- Runs OSV vulnerability scans (source and SBOM)

## 🧱 Structure
- `demo-app/` — Maven project with Log4J 2.14.1
- `.github/workflows/secure-sbom-showcase-maven.yml` — Main CI/CD workflow
- `osv-report-template.html` — Dark terminal-themed SecureSBOM CI/CD report
- `README.md` — You are here 😎

## 🚀 Usage
1. Add repository secrets:
   - `SECURE_SBOM_API_KEY`
   - `SECURE_SBOM_KEYID`
   - (GitHub automatically provides `GITHUB_TOKEN`)
2. Trigger the workflow manually under **Actions → SecureSBOM Showcase**.
3. Watch the results:
   - Signed SBOM artifacts
   - Verification pass/fail
   - OSV scan logs
   - Tamper detection
   - Pretty HTML report in summary or downloadable artifact

> **Note:** This demo intentionally includes a vulnerable dependency (Log4J 2.14.1) for educational purposes only. Do not deploy this code in production.
