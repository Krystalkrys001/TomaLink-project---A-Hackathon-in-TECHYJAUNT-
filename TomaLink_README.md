# TomaLink: Reducing Post-Harvest Tomato Losses in Nigeria

A data-backed case for a technology platform that connects Nigerian tomato farmers to cold storage, refrigerated logistics, and verified buyers. Built during the TechyJaunt Hackathon (July 2026) by a 30-person cross-functional team covering product, design, engineering, data, AI, marketing, and security.

## The Problem

Nigeria produces 3.8 to 4.0 million metric tonnes of tomatoes a year, the largest output in Sub-Saharan Africa. Despite that, 40 to 45 percent of the harvest is lost after it leaves the farm, before it ever reaches a consumer or processor. During peak harvest season, that loss rate climbs above 50 percent. The country still imports large volumes of tomato paste because so much of its own fresh harvest spoils before it can be sold.

## My Role

I worked as one of six Data Analysts on a 30-person cross-functional hackathon team. My specific contributions were:

- Sourced and researched the pilot dataset used across the project
- Cleaned the dataset: removed duplicate records and assigned the correct data type to every column, so it was analysis-ready before handing it to the Data Scientist for the predictive modelling work
- Conducted competitive research on seven existing agricultural supply chain platforms (ColdHubs, AFEX, Complete Farmer, Twiga Foods, ThriveAgric, Farmcrowdy, and ITC e-Choupal), comparing features, advantages, and weaknesses, and connecting each finding back to specific product decisions for TomaLink
- Built the team's PowerPoint presentation deck used for the final hackathon pitch
- Contributed to dashboard design and statistical validation of the pilot dataset, translating raw farm-level records into insights the product and business teams could act on

Fellow Data Analysts on this project: Suleiman Titilayo Khadijat, Eunice Istifanus Ishaku, Ogwu Joel Edike, Chiziterem Ugorji, and Orija Rasheedah. This README documents the data analysis and market research components of the project specifically.

## Data Validation

The pilot dataset (`Tomato_Supply_raw_Dataset.xlsx`) contains 5,000 farm-level records across five tomato-producing states (Jigawa, Bauchi, Plateau, Kaduna, Kano), spanning the full 2025 calendar year. It is synthetic data built on real published benchmarks (FAOSTAT, National Bureau of Statistics, and existing agricultural literature), not live production data, and the source file states this directly in every row.

Before analysis, every column was checked for internal consistency:

- 5,000 unique Farmer IDs, no duplicate records
- No missing values in any of the 39 columns
- Loss_Percentage matches the calculated value (Quantity_Lost_kg divided by Harvest_kg) in every row, with zero discrepancies
- Quantity_Sold_kg plus Quantity_Lost_kg equals Harvest_kg in every row, confirming the mass balance holds throughout
- No negative or zero values in Harvest_kg or Revenue_NGN

## Key Insights

**Weighted post-harvest loss across the pilot sits at 22.62 percent.** Out of 15,749,013 kg harvested, 3,561,795 kg never reached a buyer.

**Storage method is the single biggest lever on loss.** Open-air storage loses 30.70 percent of produce. Warehouse storage cuts that to 22.47 percent. Cold room storage brings it down to 15.58 percent, roughly half the open-air rate.

**Loss causes are spread almost evenly across five categories**, Delay (20.9 percent), Mechanical Damage (20.5 percent), Pests (20.0 percent), Heat (19.5 percent), and Poor Packaging (19.2 percent). No single fix addresses the majority of the problem. A platform that only solves storage, or only solves transport, still leaves most of the loss untouched.

**The pilot generated 10.08 billion naira in revenue and 5.90 billion naira in profit** from what was actually sold, giving a clear baseline to measure future platform impact against.

**Loss percentage stays fairly stable across the year**, generally in the low-to-mid twenties, without a single dominant seasonal spike, which suggests the loss drivers are structural (storage, transport, packaging) rather than purely seasonal.

## Recommendations

- Prioritise cold storage access as the platform's core value proposition. It has the largest single measured effect on loss reduction.
- Design the platform to address handling, timing, packaging, and storage together, not just one link in the chain, since no single cause accounts for more than 21 percent of total losses.
- Use the 22.62 percent weighted loss rate and 5.90 billion naira pilot profit as the baseline for tracking the stated business objective of a 30 percent reduction in post-harvest losses within year one.
- Track loss percentage by state going forward. Jigawa, Bauchi, Plateau, Kaduna, and Kano show similar loss rates in the pilot (22.2 to 23.0 percent), so early platform rollout in any of the five is defensible, but this should be monitored as real usage data comes in.

## Market Landscape Research

Before recommending a product direction, I researched seven existing agricultural supply chain platforms, five West or East African, one Nigerian cold storage infrastructure specialist, and one global benchmark from India, to understand what already works, what fails, and why.

| Platform | What it does | Key lesson for TomaLink |
|---|---|---|
| ColdHubs (Nigeria) | Solar powered walk-in cold storage rented by the day, no grid dependence | Cold storage should be its own dedicated service layer, not a bolted-on feature |
| AFEX (Nigeria) | Electronic warehouse receipts used as loan collateral | Built for durable grains, not perishables. Financing tomatoes needs a much shorter cycle tied to guaranteed near-term delivery, not long-term storage |
| Complete Farmer (Ghana) | Three-sided marketplace with blockchain traceability and physical fulfilment centres | A well-built app cannot outrun physical collection infrastructure. Transport and warehouse roles need as much design attention as the software |
| Twiga Foods (Kenya) | Owned its own farms, trucks, and warehouses at peak scale | The single most important cautionary tale for this project. Owning the entire chain, including farms, proved too capital-intensive and forced a 2023 to 2025 restructuring. TomaLink should connect existing stakeholders rather than own them |
| ThriveAgric (Nigeria) | Finances farmers with inputs, then links them to guaranteed offtake buyers | Pairing financing with a guaranteed buyer reduces distress selling, a direct root cause of post-harvest loss |
| Farmcrowdy (Nigeria) | Public crowdfunding of individual farms | Any public-facing investment or sponsorship feature needs full regulatory transparency from day one, or it risks losing user trust entirely |
| ITC e-Choupal (India) | Shared village internet kiosks for price data and direct sales, launched 2000 | Proves simple, low-cost technology can transform an entire supply chain nationally. Since many smallholder tomato farmers may not own a smartphone, a shared or assisted access option is worth considering alongside the mobile app |

Full platform profiles, feature breakdowns, and sourced citations are documented in `Agricultural_Supply_Chain_Platforms_Research.docx`.

## Dataset Structure

`Tomato_Supply_raw_Dataset.xlsx` contains 5,000 rows and 39 columns covering the full farm-to-market chain:

| Category | Columns |
|---|---|
| Farmer and location | Farmer_ID, State, LGA, Latitude, Longitude, Farm_Size_ha |
| Harvest | Tomato_Variety, Harvest_Date, Harvest_kg, Harvest_Season |
| Storage | Storage_Method, Storage_Days, Warehouse_ID, Cold_Storage_Available |
| Transport | Transport_ID, Vehicle_Type, Transport_km, Travel_Hours, Transport_Cost_NGN, Road_Condition |
| Conditions | Packaging, Temperature_C, Humidity_pct, Rainfall_mm |
| Sale | Buyer_Type, Buyer_ID, Market, Market_Demand_kg, Market_Price_NGN_per_kg |
| Outcome | Quantity_Sold_kg, Quantity_Lost_kg, Loss_Cause, Revenue_NGN, Estimated_Profit_NGN, Loss_Percentage |
| Status | Spoilage_Risk, Inventory_Status, Delivery_Status, GPS_Tracked, Record_Source |

## Dashboard

Built in Power BI as a diagnostic dashboard, designed to identify which links in the supply chain drive the most loss, filterable by state, buyer type, storage method, and market.

Visuals include:

- Total Harvest, Total Lost, Weighted Loss percent, Total Revenue, and Total Profit KPI cards
- Weighted loss percent by storage method
- Weighted post-harvest loss percent by state
- Weighted loss percent, cold storage available versus not
- Tomato loss by cause (donut chart)
- Transport distance versus loss percent, broken out by road condition (scatter)
- Revenue versus profit by state (combo chart)
- Loss percent trend across the year, split by dry and wet harvest season

## Tools and Skills Demonstrated

- Dataset sourcing and preparation for downstream data science work
- Data cleaning: duplicate removal and data type assignment across a 5,000-row, 39-column dataset
- Competitive and market landscape research, synthesising seven platform case studies into direct product recommendations
- Power BI dashboard design (KPI cards, filters, scatter plots, combo charts)
- Loss-driver analysis and root-cause breakdown
- Business-metric design tied to stated product objectives (loss reduction target, revenue baseline)
- Presentation design (PowerPoint deck for the final hackathon pitch)
- Cross-functional collaboration within a 30-person hackathon team spanning product, engineering, design, AI/ML, marketing, and security

## About TomaLink

TomaLink is a technology-driven post-harvest platform that connects farmers to cold storage, warehousing, logistics, and markets in one place. Rather than solving a single link in the chain, it integrates storage booking, refrigerated transport, a verified marketplace, and live shipment tracking into one connected flow, so a farmer never has to leave the platform to solve the next problem.

Stated business objectives for year one: reduce post-harvest losses by 30 percent, increase average farmer income by 20 percent, cut average farm-to-market time by 25 percent, and onboard 5,000 farmers, 1,000 buyers, 100 logistics providers, and 50 storage partners.

## Possible Next Steps

- Replace the synthetic pilot dataset with live platform usage data once TomaLink is in market, and re-run this analysis against real transactions
- Build a loss-prediction model using the existing feature set (road condition, transport distance, storage method, temperature) to flag high-risk shipments before they happen
- Track weighted loss percent by state over time as a live KPI once the platform reaches its pilot states (Kaduna, Kano, Plateau, Jos)

## License

MIT. Free to use, adapt, and build on.

---
This analysis was completed as part of the TechyJaunt Hackathon, July 2026, Group 6 (TomaLink). Dataset is synthetic, built on FAOSTAT, National Bureau of Statistics, and published agricultural literature, and does not represent live production data.
