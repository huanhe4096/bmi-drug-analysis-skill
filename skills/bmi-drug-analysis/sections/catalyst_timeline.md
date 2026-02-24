# Catalyst Timeline

## Purpose
Identify and organize the key upcoming events that could materially change the drug's
outlook. This section gives readers a forward-looking calendar of binary and incremental
catalysts, each with an estimated date and potential impact.

## Data Gathering

### BioMCP Tools
1. **`trial search`** with the drug name — filter by `RECRUITING` and
   `ACTIVE_NOT_RECRUITING` status to find trials approaching readout.
2. **`trial get`** on each relevant NCT ID — pull primary completion dates,
   estimated study completion dates, and primary endpoints.
3. **`drug get --sections approvals`** — check for pending supplemental applications
   or PDUFA dates.

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
