
[[Project-Tool-2]]


A developer deciding whether to buy a parcel with existing businesses and convert it to housing is comparing two discounted cash‑flow streams: “keep/renovate existing commercial” versus “demolish, entitle, build, lease or sell residential,” under constraints from financing, regulation, construction costs, and timing. A good Jupyter notebook can walk them line‑by‑line through this pro forma and show how assumptions about rents, costs, and delays change net present value (NPV) and feasibility.[1][2][3][4]

## 1. Current building value and rents

At acquisition, the existing building’s value is typically underwritten as the present value of its expected net operating income (NOI) from existing and future commercial tenants. Two common valuation shortcuts are:[4][5]

- **Direct capitalization:** $$ \text{Value} \approx \text{NOI} / \text{Cap Rate} $$, where NOI is stabilized net income after vacancy and operating expenses, and cap rate reflects market yields for similar properties.[5][4]
- Discounted cash flow (DCF): project annual cash flows over a hold period, add a reversion (sale) value, and discount everything back at a required return rate.[2][6]

In the notebook, you would define cells for: current rent roll by tenant, stabilized market rents per square foot, vacancy assumption, operating expense ratio, and a cap rate; then compute current value under both methods to show sensitivity to rent and cap‑rate changes.[4][5]

## 2. How rent changes drive value and finance

Because income properties are priced off income, changes in rents and occupancy directly change value. For example, a 10% increase in stabilized NOI raises value roughly 10% at a fixed cap rate, while rising interest rates or risk can widen cap rates and compress value even if rents hold steady.[3][7]

- Higher achievable commercial or residential rents increase appraised value and thus the maximum loan size under loan‑to‑value and debt‑service‑coverage constraints.[1][3]
- If rents are soft or vacancy high, the as‑is value may fall below the “land‑as‑housing” value, making demolition and conversion more attractive.[8][3]

In a notebook, you would include sliders or input cells for “current commercial rent,” “post‑renovation commercial rent,” and “post‑conversion residential rent,” then chart how value and maximum supportable loan change as those rents vary.[3][4]

### Building value and financing constraints

Lenders typically size construction and acquisition loans using:

- Loan‑to‑value (LTV): maximum loan as a share of appraised “as‑is” or “as‑complete” value.  
- Loan‑to‑cost (LTC): maximum loan as a share of total project cost.  
- Debt service coverage ratio (DSCR): net operating income must exceed annual debt service by a safety margin (e.g., 1.25×).[1][3]

The notebook can calculate, for each scenario, the appraised as‑is value, as‑complete value for the new housing, then compute maximum loan by LTV, LTC, and DSCR and highlight which constraint binds.[3][1]

## 3. Demolition, construction, and regulatory delays

Choosing conversion adds upfront negative cash flows and time delays before any new NOI arrives. Key cost and time components are:[9][8]

- Acquisition price (often linked to current building value).  
- Demolition and remediation costs, including tenant relocation or buy‑outs, hazardous materials, and site work.  
- Soft costs: architecture, engineering, legal, permitting, impact fees, and financing fees.  
- Hard costs: per‑square‑foot construction costs for the new residential building and any retained commercial podium.[8][1]
- Regulatory timeline: entitlement, design review, appeals, permit issuance, and potential inclusionary or impact‑fee obligations, often adding months or years before shovels hit the ground.[9][8]

In code, you would create a monthly or quarterly timeline: regulatory phase with soft costs only, demolition phase with negative cash flows, construction phase with drawdown of a construction loan and interest, then lease‑up and stabilization. The notebook can allow users to extend or shorten entitlement and construction durations to see the effect of delay on NPV.[7][1]

## 4. Comparing “keep as is” vs “convert to housing”

The core decision is a side‑by‑side NPV comparison:

- Scenario A: keep or modestly renovate the existing commercial building and collect commercial rents over time, plus an eventual sale price.  
- Scenario B: buy, clear, finance, build, and lease or sell the new housing (possibly with some ground‑floor retail), then exit at a future valuation.[7][3]

For each scenario, the notebook should:

- Build a timeline of cash flows: rent, operating expenses, capital expenditures, loan draws and repayments, interest, and sale proceeds.  
- Apply a discount rate that reflects the developer’s required return and risk profile.  
- Compute NPV and internal rate of return (IRR) for equity investors, both before and after leverage.[6][10][2]

The notebook can then report:

- NPV difference (Scenario B – Scenario A).  
- Break‑even land value: what you can pay for the property so that the conversion just meets your required return.  
- Required residential rent (replacement rent) given land price and cost assumptions to hit a target yield.[3]

### Example structure in the notebook (high level)

You might organize the notebook into sections:

1. Inputs: parcel size, zoning and allowable FAR, existing building area, current rent roll, market residential rents, construction and soft costs, timelines, discount rate, debt terms.  
2. As‑is commercial valuation: compute current NOI, cap‑rate value, and financed return.  
3. Conversion pro forma: entitlement and construction budget and timing, residential lease‑up and stabilized NOI, residual land value, and as‑complete value.  
4. Financing module: LTV/LTC/DSCR‑based loan sizing, interest and repayment schedule.  
5. Output dashboards: NPVs, IRRs, payback period, and sensitivity plots for rent, cost, and delay assumptions.[4][1][3]

## 5. Time value of money, changing costs, and labor

The time value of money means a dollar received in the future is worth less than a dollar received today, so long, delayed construction projects can be less attractive than steady existing income even if total future dollars are higher. Formally, each cash flow at time $$t$$ is discounted by a factor $$1/(1+r)^t$$, and the NPV is the sum of all discounted inflows and outflows.[10][11][2][6]

In the notebook, to capture dynamics over time you would:

- Apply construction cost escalation factors over the planned schedule (e.g., a yearly percentage increase in hard and soft costs).[7][8]
- Model wage and labor availability by adjusting unit construction costs or by lengthening construction duration to reflect tight labor markets.  
- Allow discount rate changes over time to reflect evolving interest rate environments or risk perceptions.  

A simple example cell could let the user specify “construction cost inflation per year,” “rent growth per year,” and “discount rate,” then recompute NPVs and show how a 12‑month entitlement delay with escalated costs and later revenues can flip a marginally feasible project into an infeasible one.[10][1]

## 6. How to turn this into a working notebook

For your final goal—a Jupyter notebook that guides an investor or developer through feasibility—the key is to make each concept above an explicit parameter, then compute and visualize outcomes. Building on standard development‑feasibility and land‑development pro‑forma templates, you can:[1][4][3]

- Start with a “Base Case” sheet in code: define all assumptions in one dictionary or DataFrame and compute a full cash‑flow table.  
- Add functions for: (a) as‑is valuation from current rents, (b) conversion cash‑flow simulation, (c) loan sizing, (d) NPV/IRR calculation.  
- Add a small set of sensitivity functions that loop over key drivers (rents, cap rate, cost per square foot, entitlement duration, discount rate) and plot NPV vs each driver.  
- Optionally integrate interactive widgets (e.g., ipywidgets) so a user can move sliders and instantly see how feasibility changes.  

If you’d like, the next step can be: I draft a concrete notebook outline with function names and example Python/Pandas code blocks you can paste directly into a .ipynb and adapt to a specific Berkeley parcel.

Sources
[1] Residential Land Development Pro Forma (Updated July 2025) https://www.adventuresincre.com/residential-land-development-model/
[2] Breaking Down Net Present Value & Its Importance to CRE Valuation https://www.altusgroup.com/insights/breaking-down-net-present-value/
[3] Chapter 11 | Development Feasibility Analysis https://textbook.getrefm.com/chapter-11-development-feasibility-analysis/
[4] The Real Estate Proforma: A Beginner's Guide - PropertyMetrics https://propertymetrics.com/blog/real-estate-proforma/
[5] Real Estate Pro-Forma: Full Guide, Excel Template, and More https://mergersandinquisitions.com/real-estate-pro-forma/
[6] Net Present Value (NPV) - Corporate Finance Institute https://corporatefinanceinstitute.com/resources/valuation/net-present-value-npv/
[7] [PDF] Development Feasibility Analysis | State Street https://www.ccdcstatestreet.com/wp-content/uploads/2020/05/State-Street-Development-Feasibility-Analysis-06-2018-v03.pdf
[8] Adaptive Reuse: Examining the Viability of Conversions https://blog.naiop.org/2023/11/adaptive-reuse-examining-the-viability-of-conversions/
[9] Feasibility Studies & Planning - Cervantes Design Associate Inc https://www.cervantesdesignassociates.com/feasibility-studies-planning.html
[10] Using Time Value Of Money For Real Estate Valuation https://leaddeveloper.com/time-value-of-money-real-estate-valuation/
[11] Net Present Value (NPV): What It Means and Steps to Calculate It https://www.investopedia.com/terms/n/npv.asp
[12] San Francisco wants to see offices turn into housing downtown. This ... https://www.bizjournals.com/sanfrancisco/news/2026/02/13/office-residential-conversions-tax-district.html
[13] Meet one tool to rule all office-to-residential conversion - Autodesk https://www.autodesk.com/design-make/articles/office-to-residential-conversion
[14] Commercial Property Office Conversion To Residential - YouTube https://www.youtube.com/watch?v=I5O3uGgxlCg
[15] Funding Your Commercial to Residential Conversions - YouTube https://www.youtube.com/watch?v=YWhl1onrLZ8
