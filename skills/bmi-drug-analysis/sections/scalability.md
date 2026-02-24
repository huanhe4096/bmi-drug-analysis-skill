# Scalability

## Purpose
Evaluate the drug's manufacturing readiness, supply chain resilience, and ability to
meet growing demand. This matters especially for drugs in high-demand categories
(obesity, Alzheimer's) or those with complex manufacturing processes.

## Data Gathering

### BioMCP Tools
1. **Drug shortage data** — active or historical shortages:
   ```
   biomcp get drug <drug> shortage
   ```
2. **Device/delivery system issues** — MAUDE data for injectables:
   ```
   biomcp search adverse-event --type device --manufacturer <company> --limit 5
   biomcp search adverse-event --type device --device "autoinjector" --limit 5
   ```

### Web Search (primary source for this section)
- Earnings call transcripts discussing capacity, CapEx, manufacturing sites
- Company press releases on manufacturing plant investments, expansions, partnerships
- FDA facility inspection reports (483 observations, warning letters)
- Industry analyses of fill-finish capacity, API supply, CDMO partnerships
- Drug shortage databases (FDA, ASHP)
- Device/delivery system supply chain (autoinjectors, pens, vials)

## Analysis Steps
1. Map the manufacturing chain:
   - API production (in-house vs. outsourced, number of sites)
   - Formulation and fill-finish (capacity utilization, expansion plans)
   - Delivery device supply (autoinjectors, pens — single source risks?)
   - Distribution and cold chain requirements
2. Assess supply vs. demand:
   - Current production capacity vs. current prescriptions
   - Planned capacity additions and their timelines
   - Demand growth projections (especially if new indications launch)
3. Identify bottlenecks:
   - Single points of failure in the supply chain
   - Regulatory risk to manufacturing sites
   - Specialized equipment or materials with limited suppliers
4. Evaluate the company's track record on execution.

## Output Subsections
- **Current manufacturing footprint**: Where and how the drug is made
- **Capacity vs. demand**: Current utilization and gap analysis
- **Expansion plans**: New facilities, partnerships, timelines, CapEx committed
- **Supply chain risks**: Bottlenecks, single-source dependencies, regulatory risk
- **Execution assessment**: Has the company delivered on past manufacturing commitments?

## Writing Notes
- Manufacturing data is often sparse — rely heavily on earnings call disclosures
  and analyst estimates
- Note when you're inferring capacity from indirect signals vs. direct disclosures
- CapEx numbers and facility timelines should be sourced to company filings
- This section may be short for early-stage drugs — that's fine, focus on what's known
