# Ship Certificate Types Reference

## Table of Contents
1. [Statutory Certificates (Flag State)](#statutory-certificates)
2. [Classification Certificates (CCS)](#classification-certificates)
3. [Insurance Certificates](#insurance-certificates)
4. [Crew Competency Certificates](#crew-competency-certificates)
5. [Common Issuers](#common-issuers)

## Statutory Certificates

### 1101 - 船舶国籍证书 (Certificate of Registry)
- **Issuer**: Flag state (e.g., Panama Maritime Authority)
- **Format**: Usually scanned image, no text layer
- **Key fields**: Certificate No., Date of Issue, Date of Expiry
- **Notes**: Panama certificates issued by SEGUMAR offices worldwide

### 1102 - 船舶最低安全配员证书 (Minimum Safe Manning Certificate)
- **Issuer**: Flag state
- **Format**: Often scanned image
- **Expiry**: Permanent — valid until crew requirements change
- **Notes**: Lists minimum number of crew by position

### 1104 - 安全管理证书 / SMC (Safety Management Certificate)
- **Issuer**: Recognized Organization (RO) on behalf of flag state
- **Format**: Text-layer PDF (when CCS-issued)
- **Key fields**: Cert No., Issue Date, Expiry (5-year cycle), Intermediate Verification
- **Annual verification**: Has intermediate verification slot (between 2nd and 3rd anniversary)

### 1105 - 油污损害民事责任保险证书 / CLC (Civil Liability Certificate)
- **Covers**: Bunker oil pollution damage (BCC) or cargo oil (CLC)
- **Issuer**: Flag state via authorized agent
- **Expiry**: Typically 1-year cycle, aligned with P&I insurance
- **Notes**: Lists insurer name and policy number

### 2222 - 国际船舶保安证书 / ISSC (International Ship Security Certificate)
- **Issuer**: Flag state or RO
- **Format**: Usually text-layer PDF
- **Key fields**: Cert No., Issue Date, Expiry (5-year cycle)
- **Annual verification**: Intermediate verification required

## Classification Certificates

These are issued by classification societies (CCS, DNV, Lloyd's, etc.) and typically have text layers.

### 1201 - 海上船舶吨位证书 (International Tonnage Certificate)
- **Based on**: Tonnage Convention 1969
- **Form**: CIT
- **Expiry**: Permanent — no expiry date
- **Key fields**: GT (Gross Tonnage), NT (Net Tonnage)

### 1202 - 海上船舶载重线证书 (International Load Line Certificate)
- **Form**: CLL
- **Expiry**: 5-year cycle
- **Annual verification**: Yes — 4 annual verification slots
- **Notes**: Look for endorsement records with surveyor signatures and dates

### 1205 - 海上船舶防止油污证书 / IOPP (International Oil Pollution Prevention Certificate)
- **Form**: COP
- **Expiry**: 5-year cycle
- **Annual verification**: Yes — includes intermediate survey
- **Appendix**: Form A (oil tankers) or Form B (non-oil-tankers) — lists equipment details
- **Notes**: Form A/B number typically matches the main certificate number

### 2205 - 货船构造安全证书 (Cargo Ship Safety Construction Certificate)
- **Form**: CSC
- **Expiry**: 5-year cycle
- **Annual verification**: Yes

### 2206 - 货船设备安全证书 (Cargo Ship Safety Equipment Certificate)
- **Form**: CSE
- **Expiry**: 5-year cycle
- **Annual verification**: Yes
- **Appendix**: Form E — equipment list

### 2207 - 货船无线电安全证书 (Cargo Ship Safety Radio Certificate)
- **Form**: CSR
- **Expiry**: 5-year cycle
- **Annual verification**: Yes (periodical inspections)
- **Appendix**: Form R — radio equipment details

### 2103 - 符合证明副本 / DOC (Document of Compliance)
- **Issued to**: The company (not the ship)
- **Form**: DOC(Flag)
- **Expiry**: 5-year cycle
- **Annual verification**: Yes — annual audit records

## Insurance Certificates

### BCC (Bunker Convention Certificate)
- **Full name**: Certificate of Insurance in Respect of Civil Liability for Bunker Oil Pollution Damage
- **Expiry**: Annual (aligned with P&I policy)
- **Issuer**: Flag state via authorized agent

### WRC (Wreck Removal Convention Certificate)
- **Full name**: Certificate of Insurance in Respect of Liability for the Removal of Wrecks
- **Expiry**: Annual (aligned with P&I policy)
- **Notes**: Not all flag states require this; may not be in the user's certificate list

## Crew Competency Certificates

### Panama Certificate of Competency (COC)
- **Document title**: "CERTIFICACIÓN DE TRÁMITE DE REFRENDO DE TÍTULO"
- **Key fields**:
  - "Nº Documento" = Certificate Number (format: E-002XXXXXXA) — THIS is what goes in the Excel
  - "Fecha de Expiración" = Expiry Date
  - CT number (e.g., CT-80080626-C8) = Processing number, NOT the certificate number
- **Language**: Spanish/English bilingual
- **Format**: Often scanned at low resolution; OCR quality varies

### GMDSS (Global Maritime Distress and Safety System)
- **Required for**: Master, Chief Officer, Second Officer, Third Officer
- **Format**: Usually same as COC — Panama-issued, bilingual

## Common Issuers

| Abbreviation | Full Name | Type |
|---|---|---|
| CCS | China Classification Society | Classification society |
| PMA | Panama Maritime Authority | Flag state |
| SEGUMAR | Segumar S.A. (Panama) | Flag state agent |
| DNV | Det Norske Veritas | Classification society |
| LR | Lloyd's Register | Classification society |
| BV | Bureau Veritas | Classification society |

### CCS Office Codes in Certificate Numbers
- SH = Shanghai
- ZS = Zhoushan
- ZJ = Zhanjiang
- RZ = Rizhao
- BE = Beihai/Fangchenggang
- TJ = Tianjin/Huanghua
- GZ = Guangzhou
