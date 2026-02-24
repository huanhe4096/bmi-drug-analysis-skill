# Financial Signal

## Purpose
Extract R&D-relevant insights from the company's financial disclosures. This isn't a
full financial analysis — it focuses specifically on what revenue, guidance, and
management commentary tell us about the drug's commercial trajectory and development
investment.

## When to Include
This section is typically activated when:
- The company recently reported quarterly or annual earnings
- Runtime instructions reference financials, revenue, or earnings
- There's a material financial event (guidance change, write-down, restructuring)

## Data Gathering

### Web Search (primary source)
- Most recent earnings press release and supplementary tables
- Earnings call transcript (management prepared remarks + Q&A)
- Company 10-Q or 10-K filing (for detailed breakdowns)
- Analyst consensus estimates (for beat/miss context)
- Investor day or R&D day presentations
- Sell-side analyst notes summarizing the quarter

### BioMCP Tools
- Generally not needed for this section, but approval context can help map revenue:
  ```
  biomcp get drug <drug> approvals indications
  ```

## Analysis Steps
1. **Revenue signal**:
   - Reported revenue vs. consensus expectations (beat/miss/in-line)
   - Sequential and year-over-year growth trajectory
   - Volume vs. price decomposition (if disclosed)
   - Geographic mix (US vs. ex-US trends)
2. **Gross-to-net dynamics**:
   - Net price realization trends
   - Rebate and discount pressure indicators
   - Channel inventory movements (stocking vs. destocking)
3. **Demand indicators**:
   - New prescription (NRx) and total prescription (TRx) trends
   - Patient funnel metrics (starts, persistency, switching)
   - Management commentary on demand signals
4. **R&D investment signal**:
   - R&D expense trends and allocation commentary
   - Pipeline investment priorities mentioned on earnings calls
   - Any programs accelerated, deprioritized, or discontinued
5. **Forward guidance**:
   - Full-year guidance revisions (raised, maintained, lowered)
   - Management confidence signals in commentary
   - Specific milestone guidance for upcoming quarters

## Output Subsections
- **Revenue trajectory**: Headline numbers with beat/miss context
- **Demand signals**: What the prescribing data tells us about real-world uptake
- **Investment priorities**: Where the company is putting R&D dollars
- **Guidance and outlook**: What management is signaling about the future
- **Key quotes**: 2–3 direct quotes from management that are particularly revealing
  (keep each quote under 15 words, use for color not substance)

## Writing Notes
- Stay focused on R&D-relevant insights — this is not a full equity research note
- Revenue numbers are facts, but interpreting them requires context (consensus,
  seasonality, channel dynamics)
- Management commentary is directional, not definitive — they have incentives to
  be optimistic
- Always note the reporting period (e.g., "Q4 2025 earnings reported January 2026")
