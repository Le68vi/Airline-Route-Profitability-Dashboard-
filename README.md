# Airline Route Profitability Dashboard | Power BI

## Project Overview

An interactive, five-page Power BI report designed to analyze airline route profitability, revenue, operating costs, passenger occupancy, aircraft performance, and seasonal demand.

The project transforms flight-level data into visual summaries that help users explore financial performance and investigate the factors associated with profitable and loss-making flights.

## Business Objectives

The report is designed to answer the following questions:

- Which routes generate the highest profit, and which incur losses?
- How do revenue, costs, and profit change over time?
- Which expense categories contribute most to total operating costs?
- How do aircraft types compare in occupancy and per-flight financial performance?
- How do season and demand level relate to passenger activity and profitability?

## Dashboard Pages

### 1. Business Overview

Provides a high-level summary of airline performance.

Key metrics and visuals:
- Total revenue, total cost, and total profit
- Overall profit margin
- Total flights and seat occupancy
- Monthly financial performance
- Top routes by profit
- Revenue and cost comparison by route category

### 2. Route Performance

Compares financial and operational performance across routes.

Key analysis:
- Profitable and loss-making routes
- Revenue versus profit margin
- Monthly route-profitability patterns
- Profit per flight
- Route-level performance summary

### 3. Revenue & Cost Analysis

Explores revenue sources and the airline's expense structure.

Key analysis:
- Ticket revenue and ancillary revenue
- Expense breakdown by cost category
- Revenue and cost per passenger
- Cost comparisons across route categories
- Reported versus calculated profit

### 4. Aircraft & Occupancy

Examines aircraft performance and passenger-capacity utilization.

Key analysis:
- Revenue and cost per flight by aircraft type
- Seat occupancy by aircraft type
- Occupancy versus profit margin
- Aircraft performance across route categories
- Cost per flight hour

### 5. Season & Demand

Explores the relationship between season, demand, and flight performance.

Key analysis:
- Passenger and occupancy trends
- Profit per flight by season
- Profit margin across season-demand combinations
- Occupancy by demand level
- Detailed flight records

## Dataset

The dataset contains flight-level operational and financial information.

| Category | Example fields |
|---|---|
| Flight information | Flight number, flight date, origin, destination, route |
| Aircraft information | Aircraft type, aircraft capacity, flight hours |
| Passenger information | Passengers, load factor |
| Business categories | Season, demand level, route category |
| Revenue | Ticket revenue, ancillary revenue, total revenue |
| Costs | Fuel, maintenance, crew, depreciation, airport fees, and other expenses |
| Financial results | Total cost, profit, profit margin |

- Dataset file: [airline_route_profitability.csv](data/airline_route_profitability.csv)
- Date range: 1 January 2024 – 31 December 2024
- Row count: 7,974 records, excluding the header row

Only share the dataset if its usage terms permit redistribution.

## Tools & Technologies

- Power BI Desktop — data modeling and interactive report development
- Power Query — data preparation and transformation
- DAX — calculated measures and business metrics
- CSV — source data format

## Data Preparation

The data-preparation workflow included:

- Reviewing column names and data types.
- Formatting flight dates for readable tables and date filtering.
- Creating a separate `FlightCosts` query for expense analysis.
- Unpivoting expense columns into `Cost_Type` and `Cost_Amount`.
- Keeping flight-level calculations separate from the unpivoted expense table.

The cost transformation changed the structure from separate expense columns into category-and-amount rows:

Before:
Flight | Fuel_Cost | Maintenance_Cost | Crew_Cost

After:
Flight | Cost_Type        | Cost_Amount
Flight | Fuel Cost        | ...
Flight | Maintenance Cost | ...
Flight | Crew Cost        | ...


This structure supports comparisons across expense categories. `Total_Cost` is not treated as an additional cost category because it already represents the supplied expense total.

Revenue, passenger counts, seat capacity, and flight counts are calculated from the original flight table to avoid duplication from the unpivoted expense rows.

## Key DAX Measures

### Total Revenue

DAX
Total Revenue =
SUM(airline_route_profitability[Total_Revenue])


### Total Cost

DAX
Total Cost =
SUM(airline_route_profitability[Total_Cost])


### Total Profit

DAX
Total Profit =
[Total Revenue] - [Total Cost]


### Profit Margin

DAX
Profit Margin % =
DIVIDE(
    [Total Profit],
    [Total Revenue]
)

### Total Passengers

DAX
Total Passengers =
SUM(airline_route_profitability[Passengers])


### Total Seats Offered

DAX
Total Seats Offered =
SUM(airline_route_profitability[Aircraft_Capacity])


### Seat Occupancy

DAX
Seat Occupancy % =
DIVIDE(
    [Total Passengers],
    [Total Seats Offered]
)

### Cost Amount

DAX
Cost Amount =
SUM(FlightCosts[Cost_Amount])

Overall profit margin is calculated from total profit divided by total revenue. Seat occupancy is calculated from total passengers divided by total seats offered, rather than by taking a simple average of flight-level percentages.

Format ratio measures as percentages without multiplying the DAX result by 100.

## Interactive Features

Keep only the features implemented in the final report:

- Five-page navigation
- Date-range slicer
- Route, aircraft, season, and demand filters
- Cross-filtering between visuals
- Tooltips with supporting metrics
- Conditional formatting
- Reset-filter button
- Synchronized slicers across pages

## Dashboard Screenshots

- Dashboard screenshots: [View all screenshots](screenshots/)

### Business Overview

[Business Overview dashboard](screenshots/business overview.png)

### Route Performance

[Route Performance dashboard](screenshots/route performance.png)

### Revenue & Cost Analysis

[Revenue and Cost Analysis dashboard](screenshots/revenue cost analysis.png)

### Aircraft & Occupancy

[Aircraft and Occupancy dashboard](screenshots/aircraft occupancy.png)

### Season & Demand

[Season and Demand dashboard](screenshots/season demand.png)


## Repository Structure

airline-route-profitability/
│
├── README.md
├── dashboard/
│   └── Airline_Route_Profitability.pbix
├── data/
│   └── airline_route_profitability.csv
├── screenshots/
│   ├── business overview.png
│   ├── route performance.png
│   ├── revenue cost analysis.png
│   ├── aircraft occupancy.png
│   └── season_demand.png


## How to Explore the Project

1. Download the Power BI report file from the `dashboard` folder.
2. Open the `.pbix` file in Power BI Desktop.
3. If refreshing the data requires a source-path update, point the source query to your local copy of the CSV.
4. Use the navigation buttons to move between pages.
5. Apply date and category filters to explore different views of performance.

## Limitations

- Results depend on the completeness and accuracy of the source dataset.
- Missing financial components may affect expense-breakdown analysis.
- Aircraft comparisons should account for differences in routes, flight duration, and operating conditions.
- Relationships shown in the report are descriptive and do not establish causation.
- Dataset provenance and currency should be documented before presenting the results as real-world airline performance.

## Skills Demonstrated

- Business-question framing
- Data transformation with Power Query
- Expense-column unpivoting
- DAX measure development
- Financial and operational KPI design
- Interactive data visualization
- Multi-page report design
- Analytical interpretation and project documentation

## Author

- Name: Mukul Kadnwal
- GitHub: https://github.com/Le68vi/Airline-Route-Profitability-Dashboard-
- LinkedIn: https://www.linkedin.com/in/mukul-kandwal-21705531a?utm_source=share_via&utm_content=profile&utm_medium=member_android
