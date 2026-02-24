# Risks and Uncertainties

## Purpose
Identify and evaluate the key risks that could negatively impact the drug's development,
commercial, or regulatory trajectory. This section is the bear case — what could go
wrong and how likely is it?

## Data Gathering

### BioMCP Tools
1. **Post-marketing safety signals** — FAERS data:
   ```
   biomcp search adverse-event --drug <drug> --serious --limit 10
   biomcp drug adverse-events <drug> --limit 10
   biomcp search adverse-event --type recall --drug <drug> --limit 5
   ```
2. **Safety publications** — meta-analyses, black box warnings, REMS:
   ```
   biomcp search article -k "<drug> safety" --since 2023-01-01 --limit 5
   biomcp search article -k "<drug> adverse events" --limit 5
   ```
3. **Failed or terminated trials** — understand what went wrong:
   ```
   biomcp search trial -c <condition> -i <drug> --status terminated --limit 5
   biomcp search trial -c <condition> -i <drug> --status suspended --limit 5
   ```
4. **Existing label warnings** — current safety information:
   ```
   biomcp get drug <drug> label
   ```

### Web Search
- FDA safety communications, MedWatch alerts, Dear Healthcare Provider letters
- Patent litigation filings and PTAB proceedings
- Congressional or political pressure on pricing
- Payer pushback (prior auth requirements, step therapy mandates)
- Manufacturing issues (483 observations, warning letters, supply disruptions)
- Short seller reports or investigative journalism raising concerns

## Analysis Steps
1. Categorize risks into:
   - **Clinical/Safety**: Adverse events, long-term safety unknowns, class effects
   - **Regulatory**: CRL risk, label restrictions, post-marketing requirements
   - **Commercial**: Pricing pressure, access barriers, patient adherence
   - **Competitive**: Market share erosion, superior competitor data
   - **Operational**: Manufacturing, supply chain, key personnel
   - **Legal/IP**: Patent challenges, litigation, regulatory exclusivity expiration
2. For each risk, assess:
   - **Likelihood**: How probable is this risk materializing? (High/Medium/Low)
   - **Impact**: If it happens, how bad is it? (Severe/Moderate/Minor)
   - **Timing**: When might this risk become relevant?
   - **Mitigants**: What reduces the probability or impact?
3. Highlight any risks that are underappreciated by the market.

## Output Subsections
- **Clinical and safety risks**: Known AEs, emerging signals, class effect concerns
- **Regulatory and legal risks**: Approval uncertainty, IP challenges
- **Commercial risks**: Pricing, access, competition, adherence
- **Operational risks**: Manufacturing, supply, execution
- **Risk matrix**: A summary table of Risk | Likelihood | Impact | Timing | Mitigants

## Writing Notes
- Don't catastrophize — assess risks proportionally
- Distinguish between theoretical risks and risks with supporting evidence
- FAERS signal-to-noise is low — note the reporting bias limitations
- Every risk claim needs evidence: "GI tolerability concerns affect ~30% of patients
  at the highest dose (SURPASS-1, Rosenstock et al., 2021)"
