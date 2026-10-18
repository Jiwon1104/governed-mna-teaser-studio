# Governed M&A Teaser Studio & Adoption Telemetry

A single-page, client-side governed application prototype built with **Claude Artifacts** (React, HTM, Vanilla CSS). Designed for M&A deal teams to safely automate anonymised buyer teaser generation within strict data protection and compliance boundaries (e.g. K3 Golden Rule and EU AI Act principles).

![Studio Preview]
<img width="2560" height="1412" alt="image" src="https://github.com/user-attachments/assets/33044f53-808d-43d7-8c92-3c7378fca4b4" />

---

## 1. Business Problem & Governance Envelope

In professional services and sell-side advisory, producing an anonymised teaser from confidential deal briefings requires intensive manual redaction.

* **Compliance Risk:** Direct input of unvetted text into LLMs risks leaking confidential client entities (names, executives, turnover, postcodes) across external model APIs.
* **Operational Inefficiency:** Manual redaction and formatting averages **90 minutes** per teaser, creating bottlenecks for fee-earners.
* **Governed Boundary:** "Zero shadow AI" and strict data isolation—confidential data must be scrubbed **at the input gate**, not fixed downstream.

---

## 2. Technical Architecture & Core Logic

### 1) In-Browser Sanitisation (Input Gate)
* **100% Client-Side Execution:** Text never leaves the browser tab (`0 bytes transmitted`).
* **Multi-Category Regex & Dictionary Tagging:**
  * **Company Identity:** Normalises corporate suffixes and extracts aliases into `[Project Codename]` and relative operating history (e.g. `[operating for 25+ years]`).
  * **Key People:** Detects founders/executives via title heuristics and masks them deterministically as `[Founder]` or `[Executive]`.
  * **Financials:** Brackets exact revenues into safe ranges (e.g. `[£12M - £16M]`), converts EBITDA into percentage margin brackets, and generalises client concentration figures.
  * **Anchor Clients & Locations:** Maps major retailers/FMCGs to generic tier descriptors and regionalises locations to `[North West England]`.
  * **Contact Details:** Automatically redacts emails, telephone numbers, postcodes, and URLs.

### 2) Residual Leak Guard & Pipeline Gate
* Runs a deterministic secondary scan across the payload. If any stem or alias of a detected entity remains unmasked, the pipeline halts and blocks model routing and clipboard export.

### 3) Deterministic Teaser Formatting
* Parses sanitised input into standard M&A sections: *Investment Thesis*, *Operational Highlights*, and *Normalised Financials* without hallucinated alterations.

### 4) Adoption Telemetry & Compliance Audit
* **Time Released Tracker:** Quantifies productivity gains (**85 minutes saved per teaser**, 94% faster).
* **Cost Governance:** Real-time token and routing simulation (Claude 3.5 Sonnet benchmark at ~£0.023 per teaser).
* **Audit Record Generation:** Produces a structured JSON audit log containing cryptographic input fingerprints, masking counts, and policy timestamps without storing original confidential text.

---

## 3. Technology Stack

* **Build Platform:** Claude Artifacts
* **Frontend:** React 18 (via UMD & HTM, standalone single-file distribution)
* **Styling:** CSS Variables with native Dark/Light mode support
* **Dependencies:** Zero external server-side dependencies; fully sandboxed.

