Berkeley already publishes most of the ingredients for a structure‑by‑structure “digital twin”; the work is to harvest, normalize, and join them into a parcel‑centric knowledge graph keyed by APN and address.[1][2][3]

## Overall ingestion and data model

- Anchor everything on a **master parcels table** (one row per parcel) with APN, address, zoning district, land use, building footprint, and geometry; this comes from the Berkeley Open Data parcel layer and Community GIS.[2][3]
- For the digital twin, design a schema where each parcel links to: permits (building, zoning, fire), ZAB actions, use permits, inspections, plans, staff reports, and any external datasets (assessor data, census, UC housing inventories).[4]

## Core city systems and document sources

- **Zoning Adjustments Board (ZAB):** Agendas, packets, minutes, and supplemental communications are published for each meeting and link to project‑level staff reports and plans; the board’s page is the entry point for bulk scraping of ZAB PDFs and metadata.[5][6]
- **Use permits:** The Use Permit page describes required applications and points to the zoning permit application process; actual records and attachments live in Permits Online / Accela (module “Zoning”) and in Building Eye as map‑linked items.[7][8][1]
- **Building and other permits:** BuildingEye and the Accela **Citizen Portal / Permits Online** expose searchable records and attached plans (PDF) for building, electrical, plumbing, mechanical, and fire permits since roughly the mid‑1990s.[8][9][4]

## Open datasets, GIS, and base maps

- **Open Data Portal:** Hosts tabular and GIS datasets for parcels, zoning, land use, business licenses, some transportation and environmental layers, all downloadable as CSV, shapefile, or GeoJSON for ingestion into your database or geospatial stack.[10][2]
- **Community GIS Portal:** Web map front‑end with layers for parcels, zoning, environmental constraints, transportation, and city facilities; some of these layers correspond to downloadable open‑data sets and provide authoritative geometries for the digital twin.[3]
- **Zoning dataset and official zoning map:** The “Zoning” GIS layer defines all zoning districts and is the authoritative source for zone boundaries; the Berkeley Municipal Code’s Official Zoning Map provides legal zoning designations for cross‑checking.[11][12]

## Permits, plans, and structural information

- **Permits Online / Accela attachments:** For each building or zoning permit record, attachments include architectural plans, structural calculations, energy compliance documentation, and inspection reports; these PDFs are accessible through Record Info → Attachments.[9][8]
- **BuildingEye:** Provides an interactive map of planning and building permits; use it to discover records by location and to cross‑walk address, permit IDs, and parcel/APN before ingesting details from Accela.[1][4]
- **Historic and non‑digitized records:** The city notes that some older permits and plans are not fully online and must be retrieved via in‑person records research or public records requests; these would need scanning and manual indexing to complete the digital twin.[13][4]

## ZAB, use permit, and staff report corpus

- **ZAB meeting packets and supplemental communications:** Each meeting packet aggregates staff reports, project plans, draft findings, conditions of approval, and public correspondence; these packets form a rich text corpus for project‑level decisions and design evolution.[6][5]
- **Staff guidance and application requirements:** The Use Permit and Zoning Permits pages link to submittal requirement documents and guides that specify what drawings and reports applicants must provide, giving a template for what to expect in each project file.[14][7]
- **Research Zoning Permits page:** The “Research zoning permits and zone designations” page explains how to use BuildingEye and the three main databases (BuildingEye, Permits Online, and Community GIS) to locate permit and zoning information for any building or parcel.[1]

## External and academic data sources

- **State and regional GIS repositories:** The California Open Data portal and state GIS hubs host additional Berkeley datasets (e.g., statewide city boundaries, environmental layers) that can be layered onto the digital twin.[15][16]
- **UC Berkeley Library GIS holdings:** The Earth Sciences & Map Library maintains parcel snapshots and other Bay Area GIS datasets that can enrich or validate city data, accessible at dedicated GIS workstations.[16]
- **Real estate and assessor data:** Public assessor sites and commercial platforms provide assessed values, building year, and sometimes unit counts keyed by APN, useful for augmenting the parcel‑level schema you already envisioned.   

## Practical ingestion and integration steps

- Use scripted crawlers to harvest ZAB agendas/packets, parse project tables inside each PDF to extract application numbers, addresses, and actions, then join those to permit IDs from Accela / BuildingEye and to APNs from the parcel dataset.[6][1]
- Pull periodic exports (or API pulls where possible) from **BuildingEye** and **Accela** to build time‑series tables of permits, inspections, and statuses; standardize on APN and normalized address as join keys across all systems.[4][8]
- Import GIS layers (parcels, zoning, land use) into a spatial database (PostGIS or SpatiaLite) and perform spatial joins so every permit, ZAB action, and document is attached to both a parcel polygon and its zoning district; this becomes the spatial backbone of the digital twin.[3][11]

This plan yields a parcel‑centric corpus where each structure and parcel in Berkeley is linked to its full regulatory, design, and permit history, ready for visualization and simulation in a Berkeley digital twin.[2][1]

Sources
[1] Research Zoning Permits and Zone Designations | City of Berkeley https://berkeleyca.gov/construction-development/land-use-development/research-zoning-permits-and-zone-designations
[2] Open Data Portal - The City of Berkeley https://berkeleyca.gov/your-government/public-records/open-data-portal
[3] Community GIS Portal https://berkeleyca.gov/city-services/community-gis-portal
[4] Can I combine data from Alameda County parcel records, the city of Berkeley parcel records, and other open source housing records for Berkeley to establish how many housing units are on each parcel https://www.perplexity.ai/search/5ffd159f-f4ed-40aa-a2b0-6f1d7a497fec
[5] Research Permit Records | City of Berkeley https://berkeleyca.gov/construction-development/permits-design-parameters/permit-process/research-permit-records
[6] Zoning Adjustments Board - The City of Berkeley https://berkeleyca.gov/your-government/boards-commissions/zoning-adjustments-board
[7] [PDF] ZONING ADJUSTMENTS BOARD - The City of Berkeley https://berkeleyca.gov/sites/default/files/legislative-body-meeting-agendas/2025-12-11_ZAB_Agenda_Linked.pdf
[8] Use Permit | City of Berkeley https://berkeleyca.gov/construction-development/permits-design-parameters/permit-types/use-permit
[9] Building Permits - City of Berkeley https://aca-prod.accela.com/BERKELEY/Cap/CapHome.aspx?module=Building&TabName=Home
[10] Permits Online | City of Berkeley https://berkeleyca.gov/construction-development/permits-design-parameters/permit-process/permits-online
[11] City of Berkeley Open Data - The City of Berkeley https://data.cityofberkeley.info
[12] Zoning | Open Data | City of Berkeley https://data.cityofberkeley.info/dataset/Zoning/iknk-w4qw
[13] Official Zoning Map - Berkeley Municipal Code https://berkeley.municipal.codes/BMC/OfficialZoningMap
[14] Berkeley Permit History Information - Megan Micco - Megan Micco https://www.meganmicco.com/blog/berkeley-permit-history/
[15] Zoning Permits | City of Berkeley https://berkeleyca.gov/construction-development/permits-design-parameters/permit-types/zoning-permits
[16] City of Berkeley - Dataset - California Open Data - CA.gov https://data.ca.gov/dataset/city-of-berkeley
[17] California & Bay Area GIS Data - UC Berkeley Library guide https://guides.lib.berkeley.edu/gis/California
[18] I need to build data schemas that allow a join on APN between different tables from different providers. Do existing real estate websites that show ownership of street addresses Also use APN numbers? What are large real estate websites https://www.perplexity.ai/search/1d07690e-7a21-4576-9a4d-331de7312800
[19] 23.402.070 Zoning Adjustments Board - Berkeley Municipal Code https://berkeley.municipal.codes/BMC/23.402.070
[20] Agenda Center - Berkeley Township https://www.berkeleytownship.org/AgendaCenter
[21] [PDF] plan commission meeting minutes march 14, 2018 - city https://www.berkeleymo.us/egov/documents/1523661115_17777.pdf
[22] [PDF] The Board of Library Trustees may act on any item on this agenda https://www.berkeleypubliclibrary.org/sites/default/files/files/inline/2010_07_14_bolt_packet.pdf
[23] Here is the December meeting schedule! We hope to see you in ... https://www.facebook.com/CityofCrownPointIN/posts/here-is-the-december-meeting-schedule-we-hope-to-see-you-in-person-at-city-hall-/1263473242489104/
[24] SF PIM | Property Information Map | SF Planning https://sfplanninggis.org/pim/
[25] Administrative Use Permit | City of Berkeley https://berkeleyca.gov/construction-development/permits-design-parameters/permit-types/administrative-use-permit
