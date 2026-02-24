# Competitive Landscape

## Purpose
Assess the drug's competitive position relative to other approved therapies and
pipeline candidates targeting the same indications. Identify who the real threats are,
where differentiation exists, and how the competitive dynamics are likely to evolve.

## Data Gathering

### BioMCP Tools
1. **All drugs for the same disease** — map the competitive set:
   ```
   biomcp disease drugs <indication>
   biomcp search drug --indication <indication> --limit 10
   ```
2. **Competitor profiles** — basic info and development stage:
   ```
   biomcp search drug -q "<competitor>" --limit 5
   biomcp get drug <competitor> targets indications approvals
   ```
3. **Competitor pipelines** — what's in their trials:
   ```
   biomcp search trial -c <condition> -i <competitor> --phase 3 --status recruiting --limit 5
   biomcp drug trials <competitor> --limit 5
   ```
4. **Head-to-head and comparative evidence**:
   ```
   biomcp search article -k "<drug> vs <competitor>" --since 2022-01-01 --limit 5
   ```

### Web Search
- Market share and prescription data (IQVIA, Symphony Health reports)
- Analyst reports comparing competitive positioning
- Company earnings calls discussing competitive dynamics
- Conference presentations with comparative data
- Pricing and access information (WAC, net price, formulary positioning)

## Analysis Steps
1. Identify the competitive set:
   - **Direct competitors**: Same mechanism, same indication
   - **Indirect competitors**: Different mechanism, same indication
   - **Emerging threats**: Pipeline candidates that could disrupt the market
2. For each competitor, assess:
   - Efficacy data (head-to-head if available, cross-trial comparison otherwise)
   - Safety/tolerability profile
   - Dosing convenience (frequency, route, titration complexity)
   - Market access (payer coverage, copay, formulary tier)
   - Label breadth (approved indications, patient populations)
3. Identify the drug's key differentiators — what makes it stand out?
4. Assess vulnerability — where could a competitor leapfrog?
5. Project how the landscape evolves over 2–3 years as pipeline drugs mature.

## Output Subsections
- **Current competitive positioning**: How the drug stacks up today
- **Key competitors deep-dive**: 2–3 most important competitors analyzed in detail
- **Emerging pipeline threats**: Earlier-stage candidates to watch
- **Differentiation assessment**: The drug's defensible advantages and vulnerabilities
- **Competitive comparison table**: Drug | Mechanism | Phase | Key Efficacy |
  Dosing | Key Differentiator

## Writing Notes
- Be fair to competitors — acknowledge their strengths, don't just cheerleader for
  the drug under analysis
- Cross-trial comparisons need heavy caveats (different populations, endpoints, etc.)
- Market share claims need sources — don't guess at prescription volumes
- Distinguish between what's approved and what's projected
