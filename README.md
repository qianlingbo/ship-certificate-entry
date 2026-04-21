# ship-certificate-entry

Hermes Agent skill — organize ship certificates and extract data into MSA/单证录入 Excel spreadsheets.

## Capabilities

**Workflow 1 — Certificate Sorting**
Sort ship certificate PDFs into standard maritime inspection order (Registry → Tonnage → Load Line → IOPP → Safety Construction/Equipment/Radio → Minimum Manning → CLC → DOC → SMC → ISSC → WRC).

**Workflow 2 — Certificate Data Extraction**
Extract certificate numbers, issue dates, expiry dates, and annual verification dates from certificate PDFs (text-layer or OCR-scanned) and populate the 单证录入 Excel template. Also extracts Panama COC competency certificate data for crew.

## Two Workflows

### 1. Certificate Sorting
Input: unsorted certificate PDFs → Output: organized folder structure with standardized filenames

```
<vessel_name>_海事/
├── 船舶证书/
│   ├── 01.INTERNATIONAL REGISTRY CERT（...）.pdf
│   └── ...
└── 适任证书/
    ├── 01.船长 <name> 适任证书.pdf
    └── ...
```

### 2. Certificate Data Extraction
Input: certificate PDFs + 单证录入 Excel template → Output: populated Excel with certificate info

## References

See [references/certificate-types.md](./ship-certificate-entry/references/certificate-types.md) for detailed certificate type codes, field mappings, and issuing organization patterns.
