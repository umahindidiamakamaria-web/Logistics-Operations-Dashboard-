# Logistics Operations Dashboard — Power BI Capstone Project

**Author:** Umahi Ndidiamaka Maria-Theresa
**Tool:** Power BI Desktop
**Project type:** End-to-end data modeling, DAX, and dashboard design

---

## Overview

This project builds a full logistics analytics solution from 14 raw relational
datasets covering drivers, trucks, trailers, customers, facilities, routes,
loads, trips, fuel purchases, maintenance records, delivery events, safety
incidents, and two pre-aggregated monthly metrics tables.

The goal was to design a working star-schema style data model from scratch,
write the DAX measures needed to answer real operational questions, and
present the results across four purpose-built dashboard pages.

## Data Source

14 CSV tables representing a fictional trucking/logistics operation:

| Table | Role |
|---|---|
| drivers, trucks, trailers, customers, routes, facilities | Dimension tables |
| loads, trips, fuel_purchases, maintenance_records, delivery_events, safety_incidents | Fact tables |
| driver_monthly_metrics, truck_utilization_metrics | Pre-aggregated monthly summaries |

Relationships were built according to a provided key relationships guide,
linking each fact table back to its relevant dimension(s) via primary/foreign
keys. 
- loads -> customers (many-to-one)
- loads -> routes (many-to-one)
- trips -> loads (one-to-one)
- trips -> drivers (many-to-one)
- trips -> trucks (many-to-one)
- trips -> trailers (many-to-one)
- fuel_purchases -> trips (many-to-one)
- maintenance_records -> trucks (many-to-one)
- delivery_events -> trips (many-to-one)
- safety_incidents -> trips (many-to-one)
  
## Data Model

- Built out full relationship mapping across all 14 tables in Power BI's Model view
- Added a custom **Date table** (`CALENDAR()` + helper columns for Year, Month Name,
  Month Number, Quarter) to support time-intelligence and consistent month-over-month
  trend charts
- Resolved several real relationship issues during modeling:
  - **Ambiguous relationship paths** between `safety_incidents`, `trips`, and `drivers`
    (multiple FK columns pointing to the same dimension) — resolved by keeping a single
    active relationship path per dimension and avoiding duplicate routes to the same table

  - A **Date/Time vs. Date** type mismatch on `purchase_date`, which caused most fuel
    purchase records to fall into an unmatched "(Blank)" bucket until the column type was
    corrected in Power Query

## DAX Measures

20+ measures were built, including:
- Core aggregates: Total Revenue, Total Trips, Total Miles, Total Fuel Gallons
- Weighted vs. naive averages: a properly mileage-weighted Avg MPG measure, rather than a
  simple average-of-averages
- Rate measures with safe division: On-Time Delivery Rate, Incident Rate per 1,000 Trips,
  Preventable Incident Rate, Maintenance Cost per Mile, Downtime Hours per 1,000 Miles
- Profitability: Route Profit, Profit Margin %, Revenue per Mile, Avg Revenue per Load

## Dashboards

Four pages, each combining related analytical use cases:

1. **Driver Performance & Safety** — on-time delivery rate, revenue per mile, MPG by
   driver, incident and preventable-incident rates
2. **Fleet & Maintenance** — miles and revenue per truck, maintenance cost per mile,
   downtime trends and cost breakdown by maintenance type
3. **Route Profitability & Fuel Efficiency** — profit margin, route-level profitability,
   fuel cost and price trends
4. **Customer & Seasonal Trends** — revenue and service levels by customer, seasonal load
   volume and rate trends over time

Each page includes KPI cards, a conditionally-formatted/sortable table, supporting charts,
and a one-line written insight summarizing the key takeaway.

## Key Findings

- Fleet-wide on-time delivery rate: **44.6%**
- Overall profit margin: **63.6%**
- ~38% of safety incidents are classified as preventable
- Load volume dips sharply every February; fuel prices peak in August
- Revenue is notably concentrated among top accounts

## Tools Used

- Power BI Desktop (data modeling, Power Query, DAX, visualization)
- Canva (final dashboard summary layout)

## Files

- `Logistics_Operations_Dashboard_Summary.png` — combined 4-dashboard summary image
- Power BI `.pbix` file (data model, measures, and all 4 report pages)

---


