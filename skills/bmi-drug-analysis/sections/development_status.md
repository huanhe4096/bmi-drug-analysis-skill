# Development Status

## Purpose
Provide a comprehensive snapshot of where the drug stands across all indications and
development programs. This is the "state of play" — what's approved, what's in trials,
what's in the pipeline, and how it all connects.

## Data Gathering

### BioMCP Tools
1. **Approved indications and regulatory history**:
   ```
   biomcp get drug <drug> indications approvals
   ```
2. **Full pipeline view** — all trials across statuses:
   ```
   biomcp drug trials <drug> --limit 15
   biomcp search trial -c <condition> -i <drug> --limit 10
   ```
3. **Trial design details** — endpoints, arms, enrollment:
   ```
   biomcp get trial <NCT_ID> arms outcomes eligibility
   ```
4. **Published results** — recent trial publications and post-hoc analyses:
   ```
   biomcp search article -k "<drug>" --since 2023-01-01 --limit 10
   biomcp get article <PMID> fulltext
   ```

### Web Search
- Company pipeline pages (often more current than ClinicalTrials.gov)
- Recent press releases on trial initiations, completions, or results
- FDA/EMA regulatory actions (approvals, CRLs, RTFs, breakthrough designations)
- Conference presentations with updated data

## Analysis Steps
1. Map the drug's full development landscape:
   - Approved indications (where, when, under what conditions)
   - Active clinical trials by phase and indication
   - Planned or announced future studies
2. For each active program, assess:
   - Trial design quality (endpoints, comparators, patient population)
   - Enrollment progress vs. timeline
   - Any interim data or signals available
3. Identify the most advanced and most important programs.
4. Note any programs that have been discontinued or paused, and why.

## Output Subsections
- **Approved indications**: Regulatory status by market (US, EU, Japan, etc.)
- **Phase 3 programs**: The pivotal trials that will drive near-term value
- **Earlier-stage pipeline**: Phase 1/2 programs with expansion potential
- **Regulatory interactions**: Recent FDA/EMA feedback, designations, or actions
- **Development timeline summary**: A concise table of Program | Phase | Status |
  Key Endpoint | Expected Readout

## Writing Notes
- Distinguish between "approved" and "under review" and "in trial" precisely
- Use NCT numbers for all referenced trials
- Note when ClinicalTrials.gov data may be stale vs. more recent company disclosures
