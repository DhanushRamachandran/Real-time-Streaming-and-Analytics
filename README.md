# Real-time-Streaming-and-Analytics
📘 Overview

This project demonstrates a real-time data streaming and analytics pipeline built on Microsoft Fabric and visualized through Power BI. The use case focuses on New York City Yellow Taxi trip data, where trip records are ingested in real time as JSON events, processed and grounded into a Fabric Eventhouse table, and then analyzed through a Power BI dashboard.

The objective is to simulate and analyze taxi operations, such as ride demand, trip duration, and revenue patterns, enabling weekly analytical insights on top of a continuous real-time data stream.
This is a ingestion heavy event-based analysis that drives the comparison about the competition between Ola and Uber taxis in the city of New York for every ride.

# Goals of the Analytics

The primary objective of this analytics project is to understand and compare the market performance and operational behavior of Ola and Uber taxis in New York City using real-time trip data.

By leveraging continuous streaming and weekly aggregated analytics, the project aims to derive actionable insights into customer demand, pricing efficiency, and competitive dynamics.

The particular analysis is done after gathering real-time data for 2,15,000 rides at NYC.

# Specific Goals

## Market Share Analysis
 Compare the total ride volume of Ola vs. Uber across time periods and city zones.
 Identify which platform dominates specific regions or time slots.
## Revenue and Fare Comparison

Evaluate the average fare per trip, tip trends, and total earnings for each company.

Understand pricing strategies and fare competitiveness.

## Demand Pattern Analysis

Identify peak hours and high-demand zones for both Ola and Uber.

## Detect patterns of customer behavior (weekdays vs. weekends, time of day, location).

## Service Efficiency & Trip Characteristics

Compare average trip durations and distances between the two providers.

Assess how efficiently each platform serves short vs. long-distance rides.

## Customer Experience Indicators

Analyze tip amounts as a proxy for customer satisfaction.

Identify correlations between trip distance, fare, and tipping behavior.

## Operational Performance Trends

Monitor weekly changes in ride count, revenue, and distance metrics.

Detect anomalies, seasonal trends, or sudden shifts in service performance.

## Competitive Benchmarking Dashboard

Build a Power BI dashboard to visualize real-time and weekly performance comparisons between Ola and Uber.

Enable decision-makers to view key performance indicators (KPIs) such as:
1. Total Rides per Platform
2. Avg Fare per Ride
3. Avg Trip Distance
4. Total Weekly Revenue
5. Customer Tip Ratios

## Strategic Market Insights

Provide insights into which service holds a competitive edge in NYC’s market.
Support business decisions for expansion, pricing optimization, and marketing strategies.

# 2. Microsoft Fabric Real-Time Streaming

🧠 2. Microsoft Fabric Real-Time Streaming (Eventhouse KQL Database)
🧩 Technology

Microsoft Fabric Real-Time Analytics — Eventhouse (KQL Database)

This component serves as the real-time ingestion, transformation, and querying layer of the project. It is built on Kusto Query Language (KQL), optimized for handling streaming telemetry and time-series data with low latency.

⚙️ Configuration



<img width="940" height="294" alt="image" src="https://github.com/user-attachments/assets/3d179b05-bc3b-4e16-ac84-79d60fc13890" />

A Fabric Eventstream is configured to ingest JSON events representing live NYC Yellow Taxi trip data from a simulated data source.

Each JSON payload corresponds to a single trip record.

The Eventstream is connected directly to a KQL Database (Eventhouse), where:

Incoming events are automatically mapped to a KQL table.

The schema (columns and datatypes) is inferred and validated upon ingestion.





🔄 Process Flow

Event Ingestion:
Real-time JSON trip events are streamed into the Eventstream service.

Routing to Eventhouse (KQL DB):
The Eventstream routes incoming data to a KQL table within the Eventhouse for continuous ingestion.


<img width="940" height="398" alt="image" src="https://github.com/user-attachments/assets/2060267d-4b66-4e04-80ef-17ed7f9ace44" />




Transformation via KQL:

KQL queries are used to clean, filter, and enrich the streamed data.

Example transformations include:

Parsing timestamps into datetime format

Deriving trip durations and fare-per-mile metrics

Tagging vendor name (Uber/Ola)



🚕 Fare Analysis Dashboard – Key Metrics & Visuals


<img width="923" height="365" alt="image" src="https://github.com/user-attachments/assets/862f744f-6bfd-4768-8e1c-91aa30538f98" />



1. Market Metrics

Fare Market Share (Pie Chart)

Purpose: Shows the proportion of total fare revenue earned by each vendor (Ola vs Uber).

Metric:

Market Share (%)
=
Vendor Fare Amount
Total Fare Amount
×
100
Market Share (%)=
Total Fare Amount
Vendor Fare Amount
	
×100

Insight: Helps identify which company dominates the fare market in NYC.

2. Temporal Fare Metrics

Average Fare over Hour (Line Chart)

Metric: Average fare amount per hour of the day for each vendor.

Purpose: Understand how fare pricing fluctuates during the day (e.g., peak vs off-peak hours).

Fare per KM over Hour (Area Chart)

Metric:

Fare per KM
=
Fare Amount
Trip Distance (km)
Fare per KM=
Trip Distance (km)
Fare Amount
	​
  
Purpose: Compares fare efficiency and pricing consistency over time between vendors.
Fare over Days (Bar Chart)
Metric: Sum of total fare amounts grouped by weekday.
Purpose: Highlights daily variations in revenue or trip frequency.

3. Weekly/Day-based Metrics

Sum of Tip Amount by Weekday (Bar Chart)
Metric: Total tip amounts grouped by weekday.
Purpose: Reveals when customers tend to tip more — indicating higher satisfaction or demand patterns.

4. Fare Composition Metrics
Fare Breakdown (Pie Chart)
Metrics Included:
Sum of fare_amount
Sum of tip_amount
Sum of tolls_amount
Sum of surcharges

Purpose: Visualizes how total ride cost is distributed across various components of a trip.

5. KPI Cards 
KPI	Formula / Metric	Meaning
68.42%	(Fare amount ÷ Total amount) × 100	Share of base fare in total revenue
11.96%	(Surcharges ÷ Total amount) × 100	Percentage contribution from surcharges
0.43%	(Airport fees ÷ Total amount) × 100	Share of airport fees in total revenue
12.58%	(Tips ÷ Total amount) × 100	Customer tip contribution percentage
2.26%	(MTA tax ÷ Total amount) × 100	MTA or city tax percentage
2.48%	(Tolls ÷ Total amount) × 100	Proportion of tolls in overall fare
2.71M	Sum of total_amount	Total revenue from all trips (aggregated)

# Key Findings
Uber holds the dominant fare market share compared to Ola, as represented in the market share pie chart.

The average fare over each hour reveals that both Ola and Uber have peaks and troughs, but Uber generally maintains higher average fares throughout the day.

Most fares are concentrated around Thursday, Friday, and Saturday, with little variation in the total fare across these days.

Fare per kilometer trends show distinct daily and hourly patterns, with Uber consistently coming out on top in fare pricing.

The fare breakdown indicates that the core fare component forms the majority of the total fare, while airport fees, surcharges, taxes, tips, and tolls collectively contribute less than 32% combined.

Saturday sees the highest sum of tip amounts by weekday, indicating a potential trend where riders tip more on weekends.

Insights
Uber’s larger market presence translates into consistently higher fares per ride and per kilometer, signaling greater pricing power or customer preference.

A significant majority (over two-thirds) of the total fare amount comes directly from the base fare, with additional components making up lesser portions, emphasizing the breakdown of ride costs for transparency.

The proportional contribution of surcharges, taxes, tips, and tolls remain relatively modest, each below 3% of the total fare, making the fare structure simple and less sensitive to these non-core fees.

The similar fare amounts across Thursday, Friday, and Saturday suggest potential uniform demand or pricing strategies on peak days.

The detailed analysis of fare, tips, and surcharges by hour and day provides actionable insights for optimizing pricing, marketing, and operational strategies.

