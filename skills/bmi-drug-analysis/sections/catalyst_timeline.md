# Catalyst Timeline

## Purpose
Identify and organize the key upcoming events that could materially change the drug's
outlook. This section gives readers a forward-looking calendar of binary and incremental
catalysts, each with an estimated date and potential impact.

## Data Gathering

### BioMCP Tools
1. **Search active trials** approaching readout:
   ```
   biomcp search trial -c <condition> -i <drug> --status recruiting --limit 10
   biomcp search trial -c <condition> -i <drug> --status active_not_recruiting --limit 10
   ```
2. **Get trial details** — pull completion dates, endpoints, and timeline:
   ```
   biomcp get trial <NCT_ID> outcomes
   biomcp get trial <NCT_ID> all
   ```
3. **Check regulatory pipeline** — pending supplemental applications or PDUFA dates:
   ```
   biomcp get drug <drug> approvals
   ```

### Web Search
- Company investor relations pages for guidance on upcoming milestones
- Conference calendars (ASCO, ADA, AHA, EASL, AASLD, ObesityWeek) for abstract
  deadlines and presentation slots
- FDA/EMA regulatory calendars for advisory committee meetings, PDUFA dates
- Earnings call transcripts for management commentary on trial timelines

## Analysis Steps
1. List all identified catalysts chronologically.
2. For each catalyst, assess:
   - **Timing**: When is it expected? How firm is the date?
   - **Type**: Binary (pass/fail readout) vs. incremental (data update, conference
     presentation, label expansion)?
   - **Impact**: If positive, what changes? If negative, what's the downside?
3. Flag any catalysts where the timing has slipped or is uncertain.
4. Note dependencies between catalysts (e.g., Phase 3 readout gates the filing).

## Output Subsections
- **Near-term catalysts** (0–6 months): Highest confidence on timing
- **Medium-term catalysts** (6–18 months): Expected but dates may shift
- **Long-term catalysts** (18+ months): Directionally known but speculative on timing
- **Catalyst risk table**: For each catalyst, one row with: Event | Expected Date |
  Type (Binary/Incremental) | Impact if Positive | Impact if Negative

## Writing Notes
- Be concrete on dates — "expected H2 2026" is better than "sometime next year"
- Distinguish between company-guided dates and analyst estimates
- Every date claim needs a source (ClinicalTrials.gov, company IR, FDA calendar)
