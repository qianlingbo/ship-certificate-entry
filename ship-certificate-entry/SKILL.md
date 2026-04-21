---
name: ship-certificate-entry
description: >
  Organize ship certificates and extract certificate information into customs/MSA
  declaration Excel spreadsheets. Handles two workflows: (1) sorting ship certificate
  PDFs into standard maritime inspection order (Registry, Tonnage, Load Line, IOPP,
  Safety Construction/Equipment/Radio, Minimum Manning, CLC, DOC, SMC, ISSC, WRC),
  and (2) extracting certificate numbers, issue dates, expiry dates, and annual
  verification dates from PDF certificates (including scanned images via OCR) to
  populate 单证录入 Excel templates. Also extracts crew competency certificate
  numbers and expiry dates for the crew list sheet.
  Use when: organizing ship certificates, sorting maritime documents, extracting
  certificate info from PDFs, filling in 单证录入 spreadsheets, 船舶证书信息录入,
  适任证书录入, maritime inspection preparation, port state control document prep,
  海事证书整理, 船舶证书排序, MSA declaration forms, 海事局申报.
---

# Ship Certificate Entry

Organize ship certificates by standard order and extract certificate data into 单证录入 Excel spreadsheets.

## Overview

This skill covers two related workflows for maritime port call document preparation:

1. **Certificate Sorting** — Rename and reorder ship certificate PDFs into the standard maritime inspection sequence
2. **Certificate Data Extraction** — Read certificate PDFs (text-layer or scanned), extract key fields, and populate the 单证录入 Excel template

Both workflows take source PDFs (typically from a USB drive or shared folder organized by vessel name) and produce organized outputs ready for MSA (海事局) submission.

## Workflow 1: Certificate Sorting

### Input
A folder of ship certificate PDFs, typically named with original numbering (e.g., `1.Registry.pdf`, `16.IOPP.pdf`).

### Standard Order
Sort and rename certificates in this sequence:

| # | Certificate | Chinese Name |
|---|-------------|-------------|
| 01 | INTERNATIONAL REGISTRY CERT | 船舶国籍证书 |
| 02 | TONNAGE CERT | 吨位证书 |
| 03 | LOAD LINE CERT (with endorsements) | 载重线证书 |
| 04 | I.O.P.P. + FORM A/B | 防油污证书 |
| 05 | SAFETY CONSTRUCTION CERT | 构造安全证书 |
| 06 | SAFETY EQUIPMENT CERT + FORM E | 设备安全证书 |
| 07 | SAFETY RADIO CERT + FORM R | 无线电安全证书 |
| 08 | MINIMUM MANNING | 最低安全配员证书 |
| 09 | CLC / BCC (Bunker Oil Pollution) | 油污责任保险证书 |
| 10 | D.O.C. (Document of Compliance) | 符合证明 |
| 11 | S.M.C. (Safety Management Certificate) | 安全管理证书 |
| 12 | I.S.S.C. (Intl Ship Security Certificate) | 国际船舶保安证书 |
| 13 | WRC (Wreck Removal Convention) | 沉船移除责任险 |

For certificates with appendix forms (IOPP+Form A/B, SE+Form E, SR+Form R), use sub-numbering: `04-1.I.O.P.P.pdf`, `04-2.I.O.P.P. FORM A.pdf`.

Preserve validity dates in filenames when present in the source: `01.INTERNATIONAL REGISTRY CERT（20210408-20260727）.pdf`.

### Crew Competency Certificates
Sort by position in this order:
1. 船长 (Master)
2. 大副 (Chief Officer)
3. 二副 (Second Officer)
4. 三副 (Third Officer)
5. 轮机长 (Chief Engineer)
6. 大管轮 (Second Engineer)
7. 二管轮 (Third Engineer)
8. 三管轮 (Fourth Engineer)

Include GMDSS certificates alongside the officer's competency certificate when present.

### Output Structure
```
<vessel_name>_海事/
├── 船舶证书/
│   ├── 01.INTERNATIONAL REGISTRY CERT（...）.pdf
│   ├── 02.TONNAGE CERT（...）.pdf
│   └── ...
└── 适任证书/
    ├── 01.船长 <name> 适任证书.pdf
    ├── 01-2.船长 <name> GMDSS.pdf
    └── ...
```

### Optional: Merge & Compress
If the user requests, merge each category into a single PDF and compress with Ghostscript:
```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook \
   -dNOPAUSE -dQUIET -dBATCH \
   -sOutputFile=output.pdf input.pdf
```
The `/ebook` setting (150dpi) balances size reduction with readability for scanned certificates.

## Workflow 2: Certificate Data Extraction & Entry

### Input
- Ship certificate PDFs (sorted or unsorted)
- Crew competency certificate PDFs (typically Panama COC — Certificate of Competency)
- 单证录入 Excel template (with sheets: 船上非旅客人员清单, 船舶证书信息, etc.)

### Step 1: Extract Ship Certificate Data

For each certificate PDF, extract:
- **证书编号** (Certificate No.)
- **签发日期** (Date of Issue) — format: YYYYMMDD
- **有效日期** (Date of Expiry) — format: YYYYMMDD, some certs are permanent (吨位, 最低配员)
- **年检日期** (Latest Annual/Intermediate Verification) — format: YYYYMMDD, take the most recent

**Extraction approach:**
1. Try `pdftotext -layout` first — works for PDFs with text layers (most CCS-issued certificates)
2. For scanned pages with no text layer (common for Registry, Minimum Manning, IOPP Form A), use OCR or vision AI to read the image
3. Parse dates from various formats: "June 15, 2021", "15/06/2021", "2021.06.15", etc. — normalize to YYYYMMDD

**Annual verification notes:**
- Look for endorsement stamps/records on the certificate pages
- Certificates may have 4-5 annual verification slots; extract the most recent date
- "NOT APPLICABLE" means no verification has been performed for that period

### Step 2: Extract Crew Competency Data

For each crew competency certificate, extract:
- **适任证书编号** — typically the "Nº Documento" field (format like E-002177070A for Panama COC)
- **有效期至** — "Fecha de Expiración" / Date of Expiry, format: YYYYMMDD

Panama COC certificates are often scanned at low resolution. If text extraction fails, use vision AI to read the certificate image. Key fields to look for:
- "Nº Documento" or "Document No." → certificate number
- "Fecha de Expiración" or "Date of Expiry" → expiry date
- The CT number (e.g., CT-80080626-C8) is a processing number, NOT the certificate number

### Step 3: Populate Excel

**船舶证书信息 sheet** — Map certificates to rows:

| Row | 证书类型代码 | Certificate |
|-----|-------------|-------------|
| 3 | 1101-船舶国籍证书 | Registry |
| 4 | 1201-海上船舶吨位证书 | Tonnage |
| 5 | 1202-海上船舶载重线证书 | Load Line |
| 6 | 1205-海上船舶防止油污证书 | IOPP |
| 7 | 2205-货船构造安全证书 | Safety Construction |
| 8 | 2206-货船设备安全证书 | Safety Equipment |
| 9 | 2207-货船无线电安全证书 | Safety Radio |
| 10 | 1102-船舶最低安全配员证书 | Minimum Manning |
| 11 | 1105-油污损害民事责任保险 | CLC/BCC |
| 12 | 2103-符合证明副本 | DOC |
| 13 | 1104-安全管理证书 | SMC |
| 14 | 2222-国际船舶保安证书 | ISSC |

Fill columns: C=证书编号, D=签发日期, E=有效日期, F=年检日期.

**船上非旅客人员清单 sheet** — Match crew by name (Column B), fill:
- Column K = 适任证书编号
- Column L = 适任证书有效期至

Only officers with competency certificates get K/L filled (船长, 大副, 二副, 三副, 轮机长, 大管轮, 二管轮, 三管轮). Ratings (水手, 机工) typically don't have COC entries.

### Date Format
The Excel template accepts dates as: `YYYYMMDD`, `YYYY/MM/DD`, or `YYYY-MM-DD`. Use `YYYYMMDD` for consistency.

## Edge Cases

- **Permanent certificates** (Tonnage, Minimum Manning): leave 有效日期 blank — these don't expire
- **Corrupted/unreadable scans**: report which certificates couldn't be read and ask the user for better scans
- **Certificate number conflicts**: some CCS certificates share the same number across different forms (e.g., Tonnage cert and Radio cert may share a number if issued in the same batch) — this is normal
- **WRC certificate**: may or may not be in the user's required list; include if present in source files
- **Multiple annual verifications**: always use the most recent date

## References

Read [certificate-types.md](./references/certificate-types.md) for detailed certificate type descriptions and common issuing patterns.
