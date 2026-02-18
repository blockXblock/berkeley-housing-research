Terner has built closely related pro‑forma tools and UrbanSim has a generic pro‑forma engine, but neither gives you a Jupyter‑first, parcel‑specific notebook that walks an individual developer through a commercial‑to‑housing conversion decision.  You can, however, borrow their structure and factors to design your own notebook that mirrors the “development math” narrative and the UrbanSim parcel feasibility logic.[1][2][3][4][5][6][7]

## 1. What Terner and UrbanSim already provide

- Terner Housing Development Dashboard & Development Calculator: browser‑based tools that take a prototype project and output developer returns and feasibility as a function of land cost, rents, parking, impact fees, etc.[8][1]
- “Making It Pencil: The Math Behind Housing Development” and its 2023 update: PDFs that walk through the core pro‑forma logic—costs, sources, income, returns—but not as code.[2][4]
- Demystifying Development Math interactive resource: a guided, step‑by‑step interactive that illustrates the developer journey and key levers; again, web UI, not notebooks.[9]
- UrbanSim parcel model and `sqftproforma` / developer model: Python‑based pro‑forma components that evaluate development feasibility for parcels based on allowed uses, prices, and costs, returning which building forms are profitable.[5][6][10]

Your notebook can sit conceptually between Terner’s project‑level calculator and UrbanSim’s parcel‑scale pro‑forma: single‑project, highly transparent, but written in Python rather than delivered as a web app.[3][7]

## 2. Notebook structure overview

**Title:**  
“Commercial‑to‑Housing Conversion Feasibility: A Step‑by‑Step Pro‑Forma in Python”  

**Sections (top‑level headings / major code blocks):**

1. Setup and base assumptions  
2. Parcel and building context  
3. “As‑Is” commercial building valuation  
4. Conversion design and cost assumptions  
5. Financing module (debt and equity)  
6. Cash‑flow timelines and NPV/IRR  
7. Sensitivity analysis (rents, costs, delays)  
8. Scenario comparison and decision summary  

Below is a concrete outline with suggested cells, variable names, and function signatures.  

***

## 3. Section‑by‑section outline

### 1. Setup and base assumptions

Narrative markdown cell: brief explanation of what the notebook does and how to use it, echoing Terner’s “development math” framing.[4][2]

Code cell (imports and global settings):

- `import numpy as np`, `import pandas as pd`, `from dataclasses import dataclass` (optional), and date/frequency settings.  
- Define a base analysis frequency and horizon, e.g. monthly periods over 15 years.  

Code cell (global financial assumptions):

- `discount_rate_annual = 0.10`  
- `rent_growth_annual = 0.02`  
- `cost_inflation_annual = 0.03`  
- Helper to convert annual to per‑period rates.  

### 2. Parcel and building context

Markdown: describe parcel‑level context similar to Terner’s “prototype project” inputs and UrbanSim parcel attributes (parcel size, zoning, FAR, allowed uses).[7][11][5]

Code cell: dictionary or small `@dataclass` for parcel info:

- `parcel = { "site_area_sf": ..., "zoning_max_far": ..., "height_limit_ft": ..., "current_building_sf": ..., "allowed_residential_far": ..., "allowed_mixed_use": True }`  

Markdown: prompt user to input or edit parcel attributes and existing commercial program (GLA, tenant count, current rent roll).  

Code cell: `existing_commercial = { "rent_psf_year": ..., "occupied_sf": ..., "vacancy_rate": ..., "op_ex_ratio": ... }`  

### 3. “As‑Is” commercial building valuation

Markdown: explain NOI, cap rate, and discounted cash flow, referencing the same concepts Terner uses in its dashboard but for an existing commercial building.[1][3]

Code cell: function to compute stabilized NOI:

- `def compute_noi(rent_psf_year, occupied_sf, vacancy_rate, op_ex_ratio): ...`  

Code cell: value via direct capitalization:

- `def cap_value(noi, cap_rate): return noi / cap_rate`  

Code cell: optional DCF over a hold period, for “keep as is” scenario:

- `def dcf_value(noi_0, growth_rate, cap_rate_exit, hold_years, discount_rate_annual): ...`  

Markdown: short explanation on how this “as‑is” value informs the land price or acquisition price and therefore the opportunity cost of demolition, echoing Terner’s “land cost” input.[2][1]

### 4. Conversion design and cost assumptions

Markdown: describe the proposed residential or mixed‑use project: number of stories, residential GFA, unit mix, parking, any retained retail, similar to a Terner prototype and UrbanSim building forms (“residential”, “mixedresidential”).[6][5][7]

Code cell: project program:

- `project = { "res_gfa_sf": ..., "units": ..., "avg_unit_sf": ..., "retail_gfa_sf": ..., "parking_stalls": ..., "construction_duration_months": ..., "lease_up_months": ... }`  

Code cell: cost assumptions:

- `costs = { "land_acquisition": ..., "demo_cost": ..., "hard_cost_res_psf": ..., "hard_cost_retail_psf": ..., "soft_cost_pct_of_hard": ..., "contingency_pct": ..., "impact_fees_per_unit": ..., "developer_fee_pct": ... }`  

Code cell: function to build a time‑phased cost schedule:

- Allocate demo, hard, and soft costs across `construction_duration_months`, applying `cost_inflation_annual`.  
- `def build_cost_schedule(project, costs, freq="M"): -> pd.DataFrame` returning a `cashflow` DataFrame with columns for each cost type and total.  

Markdown: optional note on regulatory/entitlement period where soft costs accrue but no construction yet, as highlighted in Terner’s dashboard (permitting time) and UrbanSim’s feasibility steps.[12][8]

### 5. Financing module (debt and equity)

Markdown: explain how LTV/LTC/DSCR drive debt size; Terner’s dashboard uses a target IRR and bank loan interest assumptions; UrbanSim pro‑forma likewise includes cost of capital and return thresholds.[5][1][2]

Code cell: financing assumptions:

- `finance = { "ltv_max": 0.65, "ltc_max": 0.75, "interest_rate_annual": 0.07, "loan_fees_pct": 0.01, "amort_years": 30, "interest_only_months": project["construction_duration_months"] + project["lease_up_months"] }`  

Code cell: compute total development cost (TDC):

- `def compute_tdc(cost_schedule, costs): ...`  

Code cell: loan sizing:

- `def size_loan(tdc, as_complete_value, finance, stabilized_noi):`  
  - Compute loan allowed by LTV (vs as‑complete value).  
  - Compute loan allowed by LTC (vs TDC).  
  - Optionally compute DSCR‑constrained loan given stabilized NOI.  
  - Return `loan_amount` and which constraint binds.  

Code cell: build loan draw and interest schedule during construction and lease‑up (simple interest‑only on drawn balance), then amortization post‑stabilization.  

### 6. Cash‑flow timelines and NPV/IRR

Markdown: describe the two scenarios the user will compare, similar to Terner’s and UrbanSim’s “project built vs not built” logic.[3][7][5]

Code cell: income assumptions post‑conversion:

- `income = { "res_rent_psf_year": ..., "retail_rent_psf_year": ..., "vacancy_rate_res": ..., "vacancy_rate_retail": ..., "op_ex_ratio": ..., "rent_growth_annual": rent_growth_annual }`  

Code cell: function to build revenue schedule:

- For each period after lease‑up start, calculate occupied square feet, rents, operating expenses, and NOI, adding rent growth and vacancy assumptions.  

Code cell: combine cost schedule, financing cash flows, and income schedule into a unified `cashflows` DataFrame with:

- `equity_cf` (cash flows to equity),  
- `total_project_cf` (before financing),  
- time index.  

Code cell: NPV and IRR functions:

- `def npv(rate_per_period, cashflows): ...`  
- `def irr(cashflows): ...`  

Markdown: show resulting IRR/NPV against a target developer return (Terner uses IRR thresholds to indicate whether a project “pencils”).[4][1]

### 7. As‑Is scenario and explicit comparison

Markdown: define “Scenario A: keep/renovate existing commercial,” “Scenario B: demolish and convert to housing.”  

Code cell: reuse earlier NOI and DCF functions to build a cash‑flow series for Scenario A, with:

- Current commercial NOI, simple growth, occasional capital expenditures, and an exit sale at a cap‑rate value at the end of the horizon.  

Code cell: compute NPV and IRR for Scenario A, using the same discount rate and equity cash‑flow definition.  

Code cell: compare:

- `npv_diff = npv_conversion - npv_as_is`  
- `irr_diff = irr_conversion - irr_as_is`  

Markdown: interpret: if `npv_diff > 0` and `irr_conversion > target_return`, conversion is financially more attractive; otherwise, keeping the existing building is preferred.  

### 8. Sensitivity analysis (rents, costs, delays)

Markdown: connect this to Terner’s focus on “key factors” and UrbanSim’s parcel‑level policy scenarios (density, fees, parking, permitting time).[7][8][1][5]

Code cell: one‑way sensitivity helper:

- `def sensitivity_curve(param_name, values, base_params, compute_metric_fn):`  
  - Loop over `values`, adjust parameter, recompute NPV or IRR, store results.  

Use for:

- Residential rent per square foot.  
- Hard cost per square foot.  
- Entitlement delay months.  
- Discount rate (time value of money / risk).  

Optionally: create a small DataFrame for each sensitivity and display as a table; if you later add plotting, you can graph NPV vs parameter.  

### 9. Scenario summary cell (for decision)

Markdown: “Feasibility summary” section that prints a concise table for the user.  

Code cell: print or display a summary DataFrame with:

- Rows: “As‑Is”, “Convert – Base Case”, plus any alternative schemes (e.g., “Convert with retained retail”).  
- Columns: NPV (equity), IRR (equity), peak equity required, as‑complete value, loan amount, breakeven land value, simple payback.  

This mirrors the interpretive layer Terner’s tools call “Will the project be built?” but in a transparent, editable form.[1][3][7]

***

## 4. How this ties back to Terner and UrbanSim

- Terner’s Development Calculator identifies a handful of dominant levers—land cost, construction costs, rents, fees, parking, permitting time—that you can expose as top‑level inputs and sliders in the notebook.[3][4][1]
- UrbanSim’s parcel model and `sqftproforma` treat feasibility as: for each parcel and building form, compute return given costs, prices, and regulations and mark the form as buildable if returns exceed a threshold; your notebook implements the same logic for one parcel and one or two forms (commercial vs mixed‑use residential).[6][5][7]

If you’d like, I can turn this outline into concrete skeleton code: imports, data structures, and stubbed functions ready to paste into a new `.ipynb`, with comments marking where to plug in Berkeley‑specific parcel and zoning data.

Sources
[1] Proforma - Terner Center https://ternercenter.berkeley.edu/proforma/
[2] [PDF] The Math Behind Housing Development (2023 Update) https://ternercenter.berkeley.edu/wp-content/uploads/2023/12/Development-Math-2023.pdf
[3] Gauging Development Feasibility - Local Housing Solutions https://www.localhousingsolutions.org/analyze/gauging-development-feasibility/
[4] [PDF] Making It Pencil: The Math Behind Housing Development https://ternercenter.berkeley.edu/wp-content/uploads/pdfs/Making_It_Pencil_The_Math_Behind_Housing_Development.pdf
[5] UrbanSim Cloud Platform 3.13.1 documentation https://cloud.urbansim.com/docs/general/documentation/urbansim.html
[6] Real Estate Development Models — urbansim 3.2 documentation https://udst.github.io/urbansim/developer/index.html
[7] Simulating Policy Effects on New Housing Supply in Los Angeles https://www.ternerlabs.org/blog/new-housing-supply-los-angeles
[8] Housing Development Dashboard - Terner Center - UC Berkeley https://ternercenter.berkeley.edu/research-and-policy/dashboard/
[9] Demystifying Development Math: Interactive Resource https://www.ternercenter.app/demystifying-development-math
[10] UrbanSim Parcel Model https://cloud.urbansim.com/docs/general/documentation/urbansim%20parcel%20model.html
[11] Housing Development Dashboard: Policy Gauge - Terner Center https://ternercenter.berkeley.edu/policy-gauge-dashboard/
[12] [PDF] Appendix L: Land Use Model Documentation https://www.lcog-or.gov/media/7666
[13] [PDF] Making Missing Middle Pencil: The Math Behind Small-Scale ... https://ternercenter.berkeley.edu/wp-content/uploads/2024/06/Missing-Middle-Development-Math-Final-June-2024.pdf
[14] Modeling New Housing Supply in Los Angeles - Terner Center https://ternercenter.berkeley.edu/research-and-policy/policy-dashboard-los-angeles/
[15] Affordable Housing Compares Favorably to Market-Rate Housing ... https://chpc.net/affordable-housing-compares-favorably-to-market-rate-housing-from-a-cost-perspective/
