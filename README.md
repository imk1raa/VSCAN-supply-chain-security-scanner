# VSCAN – Supply Chain Security Scanner

A Python-based supply chain security scanner that performs 9 layers of security checks on Python packages.  
Built as part of a cybersecurity seminar on **C-SCRM (Cyber Supply Chain Risk Management)**.

---

## Features

| # | Check | Description | Complexity |
|---|-------|-------------|------------|
| 1 | **CVE Check** | Scans for known vulnerabilities via OSV (Google), CVE.org (MITRE), and NVD (NIST) | Low |
| 2 | **Typosquatting Detection** | Detects suspicious package names using Levenshtein Distance | Low |
| 3 | **Hash Verification** | Compares SHA256 hash against official PyPI registry | Low |
| 4 | **Static Analysis (SAST)** | AST-based Taint Analysis — tracks data flow from Sources to Sinks | Medium |
| 5 | **Package Age** | Flags newly published, abandoned, or single-version packages | Low |
| 6 | **Transitive Dependencies** | Maps indirect dependency tree up to depth 2 | Medium |
| 7 | **URL Check** | Detects fake PyPI mirrors in requirements files | Low |
| 8 | **Maintainer Check** | Identifies account takeover signals (version gaps, major jumps) | Complex |
| 9 | **License Check** | Classifies license risk (MIT=SAFE, GPL=DANGEROUS) | Low |

---

## Output

Every scan produces three files with a timestamp:

```
scan_report_YYYYMMDD_HHMMSS.json       ← Full security report
sbom_cyclonedx_YYYYMMDD_HHMMSS.json   ← SBOM in CycloneDX 1.4 format
sbom_spdx_YYYYMMDD_HHMMSS.json        ← SBOM in SPDX 2.3 format
```

---

## Installation

```bash
git clone https://github.com/imk1raa/VSCAN.git
cd VSCAN
python -m venv .venv
.venv\Scripts\activate        # Windows
pip install requests
```

---

## Usage

**Scan a requirements file:**
```bash
python main.py requirements.txt
```

**Scan all installed packages:**
```bash
python main.py --installed
```

---

## Status Levels

```
DANGEROUS  → License forces source disclosure (GPL/AGPL)
TAMPERED   → SHA256 hash mismatch — file modified
VULNERABLE → Known CVE found
WARNING    → License requires review before commercial use
SUSPICIOUS → Typosquatting / new package / no license
SAFE       → No issues found
```

---

## APIs Used

- [OSV API](https://osv.dev) – Google Open Source Vulnerabilities
- [CVE.org](https://www.cve.org) – MITRE CVE Registry  
- [NVD API](https://nvd.nist.gov) – NIST National Vulnerability Database
- [PyPI API](https://pypi.org) – Python Package Index

---

## Standards

This project generates SBOM output compatible with:
- **CycloneDX 1.4** (OWASP) – security-focused
- **SPDX 2.3** (Linux Foundation) – license-focused

---

## Background

This scanner was built to demonstrate real-world C-SCRM concepts including:
- The SolarWinds attack vector
- The XZ Utils backdoor (2024)
- The event-stream incident

> *"Tools are not a strategy — security culture is."*

---

## Author

**Kira** – Computer Science Student, Year 4  
Cybersecurity Seminar Project, 2026
