# HSE & Risk Assessment Data Standards Landscape

A survey of existing machine-readable data models, schemas, and interchange formats for risk assessment and HSE (Health, Safety, Environment) data. Conducted April 2026.

**TL;DR:** No open, machine-readable schema exists for Bowtie risk assessments, risk registers, or most everyday HSE artifacts. Structured formats exist only where regulators mandate electronic submission or a single determined actor published one. The gap is real and significant.

---

## Bowtie-Specific Formats

**No open standard exists.** The Bowtie data model is locked inside proprietary tools:

| Tool | Vendor | Open Schema? | API? | Export |
|------|--------|-------------|------|--------|
| BowTieXP / BowTieServer | Wolters Kluwer (ex-CGE Risk) | No | REST API (licensed users only, v11+) | Visio, Excel, PDF, HTML, CSV |
| Bowtie Master / Salus Suite | Salus Technical | No | REST API (licensed users only) | Excel |
| THESIS BowTie | ABS Group | No | No | Spreadsheet |
| BowTiePro | — | No | No | Image/PDF/Word only |

The closest open schema is **Open-PSA MEF** (fault trees + event trees), but it does not model barriers as first-class entities and is designed for nuclear probabilistic safety assessment, not barrier-based risk management.

---

## Where Machine-Readable Schemas DO Exist

These are the only areas in HSE/risk with genuine, standardized, machine-readable data formats:

### Incident & Occurrence Reporting

| Standard | Domain | Format | Open? | Mandated By |
|----------|--------|--------|-------|-------------|
| **ECCAIRS E5X** | EU aviation incidents | XML/XSD (280+ fields, ADREP taxonomy) | Yes | EASA (Regulation EU 376/2014) |
| **ICAO ADREP** | Global aviation taxonomy | Coded taxonomy | Yes | ICAO member states |
| **OSHA ITA API** | US workplace injury/illness | JSON API + CSV | Yes | OSHA (establishments 100+ employees, high-hazard) |
| **NEMSIS v3** | US EMS data | XML/XSD (28 component schemas) | Yes | US national EMS standard |
| **NFIRS / NERIS** | US fire incidents | Structured data schemas | Yes | FEMA (replacing NFIRS with NERIS in 2026) |

### Chemical & Environmental Data

| Standard | Domain | Format | Open? | Mandated By |
|----------|--------|--------|-------|-------------|
| **SDScomXML (eSDScom)** | Safety Data Sheets | XML/XSD | Yes (CC BY-ND 4.0) | EU chemical industry consortium |
| **IUCLID** | REACH chemical substance data | XML/XSD (.i6z archives) | Yes | ECHA (mandatory for REACH registration) |
| **ECHA PCN** | Poison centre notifications | XML/XSD | Yes | EU (CLP Article 45) |
| **EPA Exchange Network** | US environmental compliance (TRI, NPDES, ICIS-Air, E-PRTR) | XML schemas | Yes | US EPA |

### Probabilistic Risk & Hazard Analysis

| Standard | Domain | Format | Open? | Notes |
|----------|--------|--------|-------|-------|
| **Open-PSA MEF 2.0** | Fault trees, event trees, PSA | XML (RELAX NG Compact / XSD) | Yes (open source) | Nuclear/academic. No first-class barriers. |
| **Kenexis Open PHA** | HAZOP, LOPA, SIF | JSON | Yes (vendor-published) | Single vendor schema, not an industry standard. Free desktop version. |

---

## Where There Is NOTHING

The everyday artifacts of HSE practice have **zero** standardized machine-readable formats:

### Core Risk Management

| Artifact | Status | What Exists Instead |
|----------|--------|-------------------|
| **Risk registers** | No schema | Every organization uses bespoke Excel/vendor formats |
| **Risk matrices** (5x5 likelihood/consequence) | No schema | Universal concept, zero data standardization |
| **Bowtie risk assessments** | No open schema | Proprietary tool formats (BowTieXP, etc.) |

### Process Safety & Hazard Analysis

| Artifact | Status | What Exists Instead |
|----------|--------|-------------------|
| **HAZOP worksheets** | No industry standard | Kenexis Open PHA (single vendor). Sphera PHA-Pro (market leader) has no API at all. |
| **HAZID** | No schema | Spreadsheets and proprietary tools |
| **LOPA** | No industry standard | Kenexis Open PHA only |
| **COMAH / Seveso safety reports** | No data format | Narrative documents (hundreds of pages) |

### Operational Safety

| Artifact | Status | What Exists Instead |
|----------|--------|-------------------|
| **JHA / JSA** (Job Hazard Analysis) | No schema | OSHA publishes a Word/PDF template (3-column format) |
| **SWMS** (Safe Work Method Statements) | No schema | Australian regulatory concept, digital tools use proprietary formats |
| **Permit to Work** | No schema | Every vendor has a proprietary model |
| **COSHH risk assessments** | No schema | Upstream chemical data (SDS) is standardized; workplace risk assessments are not |

### Management Systems & Regulatory

| Artifact | Status | What Exists Instead |
|----------|--------|-------------------|
| **ISO 45001 data** (OH&S management) | No data model | Process framework defining requirements, not data formats |
| **ISO 14001 data** (environmental management) | No data model | Same — management system standard, no data schema |
| **Environmental Impact Assessments** | No schema | Narrative documents in every jurisdiction |
| **RIDDOR** (UK incident reporting) | Web form only | No API, no bulk upload, no published schema |
| **CDM** (Construction Design & Management) | No data format | IFC/BIM has a minimal `PSet_Risk` property set, but nothing substantive |

### Domain-Specific

| Domain | Status | Notes |
|--------|--------|-------|
| **Mining safety (MSHA)** | Partial | Open data for retrieval (flat files on data.gov), but web-form-only submission |
| **Maritime / offshore (IMO, IOGP)** | Minimal | IOGP has structured Excel reporting templates (member-only). IMO GISIS is web forms + CSV export. NORSOK Z-013 defines methodology, not data format. |
| **SIS / SIF lifecycle** (IEC 61511) | Vendor-specific only | Kenexis Vertigo and exida exSILentia have their own formats |

---

## EHS Software Vendors

**No major vendor has published an open data model.**

| Vendor | API? | Open Schema? |
|--------|------|-------------|
| Cority | REST API | Proprietary |
| Sphera (PHA-Pro) | **No API** | Proprietary |
| Enablon (Wolters Kluwer) | Integrations | Proprietary |
| VelocityEHS | REST API | Proprietary |
| Intelex | REST API | Proprietary |
| SAP EHS | Supports SDScomXML for SDS | Broader model proprietary |
| SafetyCulture (iAuditor) | Public REST API | Proprietary inspection model |

---

## Adjacent Domains That Have Solved This

Other safety-adjacent domains have established open interchange formats, proving the model works:

| Domain | Standard | Format | What It Proved |
|--------|----------|--------|---------------|
| Cybersecurity threat intelligence | **STIX 2.1** (OASIS) | JSON | An open graph model with typed objects and relationships can become the industry standard |
| Security controls & compliance | **NIST OSCAL** | JSON/XML/YAML | Layered schema architecture (catalog, implementation, assessment) works for compliance data |
| Vulnerability advisories | **CSAF 2.0** (OASIS, now ISO/IEC 20153) | JSON Schema 2020-12 | Machine-readable advisories replaced narrative CVE descriptions |
| Healthcare risk assessment | **FHIR RiskAssessment** (HL7) | JSON | Clinical risk assessment has a standard resource type |
| Insurance catastrophe modeling | **RDOS** (Moody's RMS), **OED** (Oasis LMF) | SQL/JSON, relational | Even insurance exposure data has open schemas |
| Disaster / climate risk | **RDLS** (GFDRR / World Bank) | JSON Schema | Natural hazard metadata is standardized |

---

## The Pattern

Structured data interchange in safety/risk exists **only** when:

1. **A regulator mandates electronic submission** (OSHA, EASA, ECHA, EPA, FEMA) — this forces a schema into existence, OR
2. **A single determined actor publishes an open schema** (Open-PSA consortium, Kenexis, eSDScom consortium) — and the community adopts it because nothing else exists.

In the absence of either force, the default is Excel spreadsheets, Word documents, PDFs, and proprietary vendor databases.

---

## What This Means

The Bowtie Risk Schema in this repository is — as far as this research can determine — **the only open, published JSON Schema that models the Bowtie methodology with barriers as first-class entities**. No ISO standard, no OASIS standard, no vendor, and no open-source project provides an equivalent.

The opportunity extends beyond Bowtie: a family of open schemas covering the core HSE data types (risk registers, HAZOP, JHA, LOPA, permits) would address a gap that affects every safety-critical industry.
