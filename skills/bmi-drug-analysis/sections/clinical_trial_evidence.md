# Clinical Trial Evidence

## Purpose
Provide a deep, data-rich analysis of the drug's key clinical trial results. While
Development Status covers the pipeline overview, this section digs into the actual
evidence — the numbers, the effect sizes, the statistical rigor, and what the data
really shows.

## Data Gathering

### BioMCP Tools
1. **Find all trials** for the drug — pivotal and supportive:
   ```
   biomcp drug trials <drug> --limit 15
   biomcp search trial -c <condition> -i <drug> --limit 10
   ```
2. **Get trial details** — results, endpoints, arms, demographics:
   ```
   biomcp get trial <NCT_ID> outcomes arms
   biomcp get trial <NCT_ID> all
   ```
3. **Published trial results** — full papers have richer data than registries:
   ```
   biomcp search article -k "<drug> phase 3" --since 2022-01-01 --no-preprints --limit 10
   biomcp search article -k "<drug> randomized" --since 2022-01-01 --limit 5
   ```
4. **Full article details** — specific numerical outcomes and methodology:
   ```
   biomcp get article <PMID> fulltext
   biomcp get article <PMID> annotations
   ```

### Web Search
- Published trial results in major journals (NEJM, Lancet, JAMA)
- Conference presentations with data (poster PDFs, oral presentation slides)
- FDA review documents (contain detailed statistical reviews)
- Advisory committee briefing documents
- Post-hoc analyses and subgroup publications

## Analysis Steps
1. Identify the most important trials:
   - Pivotal Phase 3 trials that supported or will support approval
   - Head-to-head comparisons vs. standard of care or competitors
   - Key Phase 2 trials with proof-of-concept data for new indications
2. For each key trial, extract and analyze:
   - **Primary endpoint results**: Effect size, confidence interval, p-value
   - **Key secondary endpoints**: Clinically meaningful secondary outcomes
   - **Response rates**: Proportion of patients achieving thresholds
   - **Safety data**: Adverse event rates, discontinuation rates, serious AEs
   - **Patient population**: Who was studied (inclusion/exclusion, demographics)
   - **Comparator**: What was the control arm and was it appropriate?
3. Assess the quality and reliability of the evidence:
   - Were trials adequately powered?
   - Is the effect size clinically meaningful (not just statistically significant)?
   - How does the data compare to the therapeutic area benchmarks?
   - Are there concerning signals in subgroup analyses?
4. Synthesize across trials — is the evidence consistent?

## Output Subsections
- **Pivotal trial results**: The trials that matter most, analyzed in depth
- **Efficacy profile summary**: Consistent effect sizes and response rates across
  the program
- **Safety and tolerability**: AE profile, discontinuation rates, long-term data
- **Cross-trial consistency**: Does the drug deliver reliably across populations?
- **Evidence quality assessment**: Strengths and limitations of the data package
- **Key data table**: Trial Name | N | Primary Endpoint | Result | Comparator |
  Key Safety Finding

## Writing Notes
- Numbers are the backbone of this section — be precise with effect sizes,
  confidence intervals, and p-values
- Always state the comparator and patient population when quoting results
- Distinguish between intention-to-treat (ITT) and per-protocol analyses
- Phase 2 data is hypothesis-generating — don't overweight it vs. Phase 3
- Cross-trial comparisons need caveats about different populations and designs
