# BioMCP Tool Usage Guide

BioMCP is a single-binary CLI and MCP server for querying biomedical databases.
This guide covers the tools most relevant to drug R&D analysis, organized by entity.

## Global Options

- `--json` — return structured JSON output (place before subcommand: `biomcp --json get drug ...`)
- `--no-cache` — bypass HTTP cache for the current command

## Command Grammar

Two core patterns:
```
biomcp search <entity> [filters]       # discovery across entities
biomcp get <entity> <id> [sections]    # focused detail retrieval
```

Plus cross-entity helpers:
```
biomcp <entity> <helper> <id>          # pivot between related entities
```

---

## Drug

### Search
```bash
biomcp search drug -q "tirzepatide" --limit 5
biomcp search drug --target GLP1R --limit 5
biomcp search drug --indication obesity --limit 5
```

### Get (basic record — identity and mechanism)
```bash
biomcp get drug tirzepatide
```

### Get with sections
| Section | Command | Returns |
|---------|---------|---------|
| Targets | `biomcp get drug tirzepatide targets` | Molecular targets, mechanism |
| Indications | `biomcp get drug tirzepatide indications` | Approved and investigational indications |
| Approvals | `biomcp get drug tirzepatide approvals` | FDA/EMA approval history |
| Label | `biomcp get drug tirzepatide label` | FDA prescribing information |
| Shortage | `biomcp get drug tirzepatide shortage` | Drug shortage reports |
| Interactions | `biomcp get drug tirzepatide interactions` | Drug interactions |
| CIViC | `biomcp get drug tirzepatide civic` | CIViC clinical evidence |

### Cross-entity helpers
```bash
biomcp drug trials tirzepatide --limit 5       # find trials for this drug
biomcp drug adverse-events tirzepatide --limit 5  # find adverse events
```

**Use for**: Development Status, Competitive Landscape, Scalability sections.

---

## Trial

### Search
```bash
biomcp search trial -c "type 2 diabetes" --status recruiting --limit 5
biomcp search trial -c obesity -i tirzepatide --limit 5
biomcp search trial -c obesity --phase 3 --status recruiting --limit 5
```

| Filter | Flag | Example |
|--------|------|---------|
| Condition | `-c` | `-c "type 2 diabetes"` |
| Intervention | `-i` | `-i tirzepatide` |
| Status | `--status` | `recruiting`, `active_not_recruiting`, `completed` |
| Phase | `--phase` | `1`, `2`, `3`, `4` |
| Biomarker gene | `--biomarker` | `--biomarker BRAF` |
| Mutation | `--mutation` | `--mutation "BRAF V600E"` |
| Geographic | `--lat`, `--lon`, `--distance` | Location-based filtering |
| Source | `--source` | `ctgov` (default) or `nci` |
| Limit | `--limit` | Max results |
| Offset | `--offset` | Pagination |

### Get trial details
```bash
biomcp get trial NCT05556512
```

### Get with sections
| Section | Command | Returns |
|---------|---------|---------|
| Eligibility | `biomcp get trial NCT05556512 eligibility` | Inclusion/exclusion criteria |
| Locations | `biomcp get trial NCT05556512 locations` | Study sites |
| Outcomes | `biomcp get trial NCT05556512 outcomes` | Primary/secondary endpoints |
| Arms | `biomcp get trial NCT05556512 arms` | Treatment groups |
| References | `biomcp get trial NCT05556512 references` | Related publications |
| All | `biomcp get trial NCT05556512 all` | Everything |

**Use for**: Catalyst Timeline, Development Status, Clinical Trial Evidence sections.

---

## Adverse Event

### Search FAERS (drug safety reports)
```bash
biomcp search adverse-event --drug tirzepatide --limit 5
biomcp search adverse-event --drug tirzepatide --serious --limit 5
biomcp search adverse-event --drug tirzepatide --reaction nausea --limit 5
```

### Search recalls
```bash
biomcp search adverse-event --type recall --drug tirzepatide --limit 5
biomcp search adverse-event --type recall --drug tirzepatide --classification I --limit 5
```

### Search device events (MAUDE)
```bash
biomcp search adverse-event --type device --device "autoinjector" --limit 5
biomcp search adverse-event --type device --manufacturer "Eli Lilly" --limit 5
```

### Get report details
```bash
biomcp get adverse-event <report_id>
```

| Section | Returns |
|---------|---------|
| `reactions` | Adverse reactions reported |
| `outcomes` | Outcomes (death, hospitalization, etc.) |
| `concomitant` | Concomitant medications |
| `guidance` | Safety guidance and labeling |
| `all` | All sections |

**Use for**: Risks and Uncertainties section.

---

## Article

### Search
```bash
biomcp search article -g GLP1R -d obesity --limit 5
biomcp search article -k "tirzepatide phase 3" --limit 5
biomcp search article -k "tirzepatide" --since 2024-01-01 --limit 5
biomcp search article -k "GLP-1 agonist obesity" --since 2024-01-01 --no-preprints --limit 5
```

| Filter | Flag | Example |
|--------|------|---------|
| Gene | `-g` | `-g GLP1R` |
| Disease | `-d` | `-d obesity` |
| Keyword | `-k` | `-k "tirzepatide weight loss"` |
| Since date | `--since` | `--since 2024-01-01` |
| Exclude preprints | `--no-preprints` | Peer-reviewed only |
| Limit | `--limit` | Max results |
| Offset | `--offset` | Pagination |

### Get article (accepts PMID, PMCID, or DOI)
```bash
biomcp get article 37385644
biomcp get article 37385644 fulltext       # full text if available
biomcp get article 37385644 annotations    # entity annotations
```

### Helper: extract annotated entities
```bash
biomcp article entities 37385644           # PubTator entity extraction
```

**Use for**: All sections — cite primary literature for clinical data claims.

---

## Disease

### Search
```bash
biomcp search disease -q obesity --limit 5
biomcp search disease -q "type 2 diabetes" --source mondo --limit 5
```

### Get disease record
```bash
biomcp get disease obesity
biomcp get disease MONDO:0011122
```

### Get with sections
| Section | Returns |
|---------|---------|
| `genes` | Gene associations with relationship/source |
| `phenotypes` | HPO phenotypes with qualifiers |
| `variants` | Disease-associated variants |
| `models` | Model organism evidence |
| `pathways` | Associated pathways |
| `prevalence` | Population prevalence statistics |
| `civic` | CIViC clinical evidence |
| `all` | Everything |

```bash
biomcp get disease obesity genes phenotypes
biomcp get disease MONDO:0011122 all
```

### Cross-entity helper
```bash
biomcp disease drugs obesity                # all drugs for this disease
```

**Use for**: Competitive Landscape (finding all drugs for an indication).

---

## Gene

### Search
```bash
biomcp search gene -q GLP1R --limit 5
```

### Get gene record
```bash
biomcp get gene GLP1R
```

### Get with sections
| Section | Returns |
|---------|---------|
| `pathways` | Pathway associations |
| `diseases` | Disease relationships |
| `ontology` | Ontology term mappings |
| `protein` | Protein summary |
| `go interactions` | GO terms and protein interactions |
| `civic` | CIViC evidence |

```bash
biomcp get gene GLP1R pathways diseases
```

### Cross-entity helpers
```bash
biomcp gene trials GLP1R --limit 5
biomcp gene drugs GLP1R --limit 5
biomcp gene pathways GLP1R
biomcp gene articles GLP1R
biomcp gene definition GLP1R
```

**Use for**: Understanding drug mechanism and target biology.

---

## Variant

### Search
```bash
biomcp search variant -g BRAF --hgvsp V600E --limit 5
biomcp search variant -g BRCA1 --significance pathogenic --limit 5
biomcp search variant -g BRCA1 --max-frequency 0.01 --min-cadd 20 --limit 5
```

### Get (accepts rsID, HGVS, or gene-protein form)
```bash
biomcp get variant "BRAF V600E"
biomcp get variant rs113488022
biomcp get variant "chr7:g.140453136A>T"
```

### Get with sections
| Section | Returns |
|---------|---------|
| `predict` | Predictive scores |
| `clinvar` | ClinVar annotations |
| `population` | Population genetics |
| `civic` | CIViC entries |
| `gwas` | Trait associations |
| `conservation` | GERP/phyloP scores |
| `cosmic` | Somatic mutation data |
| `cbioportal` | Frequency data |
| `all` | Everything |

### Helpers
```bash
biomcp variant trials "BRAF V600E"
biomcp variant oncokb "BRAF V600E"         # requires ONCOKB_TOKEN
biomcp variant articles "BRAF V600E"
```

---

## Protein

### Search
```bash
biomcp search protein -q GLP1R --limit 5
```

### Get (by UniProt accession)
```bash
biomcp get protein P43220
```

### Get with sections
| Section | Returns |
|---------|---------|
| `domains` | Protein domains |
| `interactions` | Protein-protein interactions |
| `structures` | PDB/AlphaFold structure IDs |

```bash
biomcp protein structures P43220
```

---

## Pathway

### Search
```bash
biomcp search pathway -q "GLP-1 signaling" --limit 5
```

### Get (by Reactome ID)
```bash
biomcp get pathway R-HSA-5673001
```

### Get with sections
| Section | Returns |
|---------|---------|
| `genes` | Associated genes |
| `events` | Contained biochemical events |
| `enrichment` | Gene-set enrichment analysis |

### Cross-entity helpers
```bash
biomcp pathway drugs R-HSA-5673001 --limit 5
biomcp pathway articles R-HSA-5673001
biomcp pathway trials R-HSA-5673001
```

---

## Organization (search-only)

```bash
biomcp search organization -q "Eli Lilly" --limit 5
biomcp search organization --type industry --city Indianapolis --limit 5
biomcp search organization --type academic --state Massachusetts --limit 10
```

| Flag | Description |
|------|-------------|
| `-q` | Name or keyword |
| `--type` | `academic` or `industry` |
| `--city` | City filter |
| `--state` | State/province filter |
| `--limit` | Max results |

Data sourced from NCI Clinical Trials Search API.

---

## Intervention (search-only)

```bash
biomcp search intervention -q tirzepatide --limit 5
biomcp search intervention --type drug --limit 10
biomcp search intervention --type drug --category "GLP-1 receptor agonist" --limit 5
biomcp search intervention --code C1447 --limit 5
```

| Flag | Description |
|------|-------------|
| `-q` | Name or keyword |
| `--type` | `drug`, `device`, or `procedure` |
| `--category` | Category filter |
| `--code` | NCI thesaurus code |

---

## Biomarker (search-only)

```bash
biomcp search biomarker -q GLP1R --limit 5
biomcp search biomarker --type "Gene" --limit 5
biomcp search biomarker --eligibility inclusion --limit 10
biomcp search biomarker --assay-purpose "Eligibility Criterion - Inclusion" --limit 5
biomcp search biomarker --code C17965 --limit 5
```

---

## Batch Mode

Run the same query across multiple IDs in parallel:
```bash
biomcp batch gene GLP1R,GIPR --sections pathways,diseases
biomcp batch trial NCT05556512,NCT04184622
biomcp batch variant "BRAF V600E","KRAS G12D" --json
biomcp batch drug tirzepatide,semaglutide --sections targets,indications
```

---

## Enrichment

Gene-set enrichment analysis:
```bash
biomcp enrich GLP1R,GIPR,GCG,GLP1 --limit 10
```

---

## Strategy for Drug R&D Analysis

For each report section, here's the recommended BioMCP tool combination:

### Catalyst Timeline
1. `biomcp search trial -c <condition> -i <drug> --status recruiting` — active trials
2. `biomcp get trial <NCT_ID> outcomes` — endpoints and expected dates
3. `biomcp get drug <drug> approvals` — pending regulatory actions
4. WebSearch — company IR, conference calendars, PDUFA dates

### Development Status
1. `biomcp get drug <drug> indications approvals` — what's approved where
2. `biomcp drug trials <drug> --limit 10` — full pipeline view
3. `biomcp get trial <NCT_ID> arms outcomes` — trial design details
4. WebSearch — press releases, pipeline page updates

### Competitive Landscape
1. `biomcp disease drugs <indication>` — all drugs for the same disease
2. `biomcp search drug --indication <indication> --limit 10` — broader search
3. `biomcp get drug <competitor> targets indications approvals` — competitor profiles
4. `biomcp search trial -c <condition> --phase 3 --status recruiting` — competing trials
5. WebSearch — market share data, pricing, analyst comparisons

### Clinical Trial Evidence
1. `biomcp drug trials <drug> --limit 10` — find all trials
2. `biomcp get trial <NCT_ID> outcomes arms` — detailed results
3. `biomcp search article -k "<drug> phase 3" --since 2022-01-01 --limit 10` — published results
4. `biomcp get article <PMID> fulltext` — full paper details

### Risks and Uncertainties
1. `biomcp search adverse-event --drug <drug> --serious --limit 10` — FAERS safety data
2. `biomcp search adverse-event --type recall --drug <drug> --limit 5` — recalls
3. `biomcp get drug <drug> label` — existing safety warnings
4. `biomcp search article -k "<drug> safety" --since 2023-01-01 --limit 5`
5. WebSearch — FDA safety communications, patent litigation, pricing pressure

### Scalability
1. `biomcp get drug <drug> shortage` — current or historical shortages
2. `biomcp search adverse-event --type device --manufacturer <company> --limit 5` — device issues
3. WebSearch — earnings transcripts (primary source), manufacturing announcements, CapEx

### Financial Signal
1. WebSearch — earnings press releases, transcripts, 10-Q/10-K filings (primary)
2. `biomcp get drug <drug> approvals` — contextualize revenue lines

### Limitations & Staleness
1. Review data recency from all other sections
2. `biomcp search article -k "<drug>" --since <30_days_ago> --limit 5` — very recent news
3. WebSearch — last 30 days for anything sections may have missed

## Citing BioMCP Data

When citing data retrieved through BioMCP, use these formats:

- **Clinical trials**: "ClinicalTrials.gov, NCT05556512, accessed YYYY-MM-DD"
- **PubMed articles**: "Author et al., Journal, Year. PMID: 12345678"
- **FDA approvals**: "Drugs@FDA, NDA/BLA number, approval date"
- **FAERS data**: "FDA FAERS database, query: <drug>, accessed YYYY-MM-DD"
- **Drug shortage**: "FDA Drug Shortages Database, accessed YYYY-MM-DD"
- **Disease ontology**: "Monarch Initiative / MONDO, accessed YYYY-MM-DD"
- **Protein data**: "UniProt accession P43220, accessed YYYY-MM-DD"
- **Pathway data**: "Reactome R-HSA-XXXXXXX, accessed YYYY-MM-DD"
