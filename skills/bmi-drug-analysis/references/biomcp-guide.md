# BioMCP Tool Usage Guide

BioMCP is an MCP server that provides access to biomedical databases. Use these tools
to gather structured data for drug analysis sections. This guide covers the most
relevant tools for drug R&D analysis.

## Drug Information

### Search for a drug
```
biomcp drug search --name "tirzepatide"
```
Returns: Drug identifiers, basic info, known names/synonyms.

### Get drug details
```
biomcp drug get --name "tirzepatide" --sections targets,indications,approvals
```
Available sections:
- `targets` — Molecular targets and mechanism of action
- `indications` — Approved and investigational indications
- `approvals` — FDA/EMA approval history and dates
- `label` — Prescribing information highlights
- `shortages` — Drug shortage reports (if any)

Use this for: Development Status, Competitive Landscape sections.

## Clinical Trials

### Search trials for a drug
```
biomcp trial search --query "tirzepatide" --status "RECRUITING,ACTIVE_NOT_RECRUITING,COMPLETED"
```
Key parameters:
- `--query`: Drug name or condition
- `--status`: Filter by trial status
- `--phase`: Filter by phase (1, 2, 3, 4)

### Get trial details
```
biomcp trial get --nct_id "NCT05556512"
```
Returns: Full trial record — design, endpoints, enrollment, dates, results.

Use this for: Catalyst Timeline, Development Status sections.

## Adverse Events

### Search adverse events for a drug
```
biomcp drug adverse-events --name "tirzepatide"
```
Returns: FAERS data — reported adverse events, frequencies, signals.

Use this for: Risks and Uncertainties section.

## Scientific Literature

### Search articles
```
biomcp article search --query "tirzepatide phase 3 obesity"
```
Returns: PubMed results with PMIDs, titles, abstracts.

### Get article details
```
biomcp article get --pmid "12345678"
```
Returns: Full article metadata, abstract, MeSH terms.

Use this for: All sections — cite primary literature for clinical data claims.

## Disease and Target Context

### Search disease associations
```
biomcp disease search --query "obesity"
biomcp disease drugs --disease "obesity"
```
Returns: Disease-drug associations, approved therapies.

Use this for: Competitive Landscape section.

### Gene/target info
```
biomcp gene search --query "GLP1R"
biomcp gene get --symbol "GLP1R" --sections summary,drugs
```
Returns: Gene function, associated drugs, pathways.

Use this for: Understanding mechanism and competitive differentiation.

## Strategy for Data Gathering

For each section type, here's the recommended BioMCP + WebSearch combination:

### Catalyst Timeline
1. `biomcp trial search` — find active/upcoming trials
2. `biomcp trial get` — get expected completion dates and milestones
3. `WebSearch` — company IR pages, conference presentations, analyst day transcripts

### Development Status
1. `biomcp drug get --sections indications,approvals` — approval status
2. `biomcp trial search` — full pipeline view
3. `WebSearch` — recent press releases, FDA correspondence

### Competitive Landscape
1. `biomcp disease drugs` — all drugs for the same indication
2. `biomcp drug search` for each competitor — get their stage/status
3. `biomcp trial search` for competitors — compare trial designs
4. `WebSearch` — head-to-head data, analyst comparisons, market share

### Risks and Uncertainties
1. `biomcp drug adverse-events` — safety signal data
2. `biomcp article search` — safety publications, meta-analyses
3. `WebSearch` — FDA warnings, patent litigation, pricing controversies

### Scalability
1. `WebSearch` — earnings transcripts, manufacturing announcements, supply updates
2. `biomcp drug get --sections shortages` — supply issues

## Citing BioMCP Data

When citing data from BioMCP, use these formats:

- Clinical trials: "ClinicalTrials.gov, NCT05556512, accessed 2026-02-24"
- PubMed articles: "Author et al., Journal, Year. PMID: 12345678"
- FDA data: "Drugs@FDA, NDA/BLA number, approval date"
- FAERS data: "FDA FAERS database, accessed 2026-02-24"
- Drug databases: "ChEMBL/MyChem.info, accessed 2026-02-24"
