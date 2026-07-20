# Smart_City_Bike_Sharing_Data_Analysis
# Description
Public bike-sharing systems generate continuous data from hundreds of stations across different cities. The task is to analyze this real-time bike station dataset to understand station performance, usage efficiency, and operational patterns across cities.
# Data Sources 
  ●	Source: Dataset link 
  ●	Timeline: 2022 - 2025
  ●	Domain: Smart City Development
# Tools & Technologies
  ●	Power Query: Data cleaning, transformations.
  ●	Power BI: Data modelling, DAX calculations, visualization, and interactive dashboard creation.
# Data Pre-Processing (Power Query)
  Tasks Performed:
  ●	Data Cleaning & Transformation: Standardized formats, and created calculated fields and columns.
  ●	Filtering & Sorting: Organized data to focus on relevant records.
# Data Modelling and DAX (Power BI) 
  ●	Data Model: Established relationships between tables Fact_Bike_Stand, Dim_Station and Date table defined cardinality.
# Calculated Columns & DAX Measures: Implemented DAX formulas for key metrics are
o	Active_Bike_Station_Count = 
        CALCULATE(
        COUNTROWS(Fact_Bike_Stand),
        Fact_Bike_Stand[Available Bike Stands] <> 0
        )
o	Avg Capacity - Banking App/Member only = 
        CALCULATE(
        AVERAGE(Dim_Station[Bike Stands]),
        Dim_Station[Banking] = "FALSE"
        )
o	Avg Capacity - Banking Enabled = 
        CALCULATE(
        AVERAGE(Dim_Station[Bike Stands]),
        Dim_Station[Banking] = "TRUE"
        )
o	Communication_Status = 
        IF([Minutes_Since_Last_Update] > 30, "🚨 Stale Data (Offline)", "✅ Live Data (Online)")
o	Inactive_Bike_Station_Count =
        CALCULATE(
        COUNTROWS(Fact_Bike_Stand),
        Fact_Bike_Stand[Available Bike Stands] = 0
        )
o	Last_Reported_Timestamp = MAX(Fact_Bike_Stand[Last Update])

o	Percentage of Bonus Stations = 
        DIVIDE(
        CALCULATE(
        COUNTROWS(Dim_Station), 
        Dim_Station[Bonus] = "True"
        ),
        COUNTROWS(Dim_Station),
        0
        )
o	Percentage of Operational Stations = 
        DIVIDE(
        CALCULATE(
        COUNTROWS(Fact_Bike_Stand),
        Fact_Bike_Stand[Status] = "OPEN"
        ),
        COUNTROWS(Fact_Bike_Stand),
        0
        )
o	Total_Network_Stands = SUM(Dim_Station[Bike Stands])
o	Data model done by separating the raw data set into fact and dimension tables, and the date table is created.
o	One Measurable table is created to align and identify all measures easily.
o	One calculated text column was created in the Fact_Bike_Stand table to clean the Name column. 
o	One unnecessary column named Number was removed.
o	Custom columns are added for separate Date and Time.
# ●	Key Findings: 
Network Architecture & Top Clusters
    o	Total Network Stations: ~3,000 active locations
    o	Top High-Density Cluster Capacity: 1,236 total bike stands (Toulouse urban center)
    o	Station 1 (43.60, 1.45): 439 stands
    o	Station 2 (43.61, 1.45): 407 stands
    o	Station 3 (43.61, 1.44): 390 stands
 Incentive & Terrain Management
    o	Bonus Location Distribution: 2.45% of the entire network
    o	Total Active Bonus Stations: 57 stations (targeted at extreme geographic choke points/inclines)
💳 Hardware & Asset Capacity
    o	Average Capacity (Terminal-Free Stations): 20.19 stands per station
    o	Average Capacity (With Banking Terminals):
    o	18.85 stands per station
    o	Capacity Increase via Digitization: +1.34 stands on average (+7.1% capacity growth per terminal-free station)
🔧 Operational Health & Maintenance
    o	Global Operational Health Rate: 92.82% fully functional
    o	Global System Outage Rate: 7.18% offline
    o	Total Offline Infrastructure: 205 stations out of service
    o	Target Operational Threshold: >95.00% (Industry Gold Standard)
    o	Critical Isolation Radius: 1.5 km (High-priority threshold for geographically isolated offline stations)
🌍 Flagship Market Concentrations
    o	Top 2 Flagship Contract Capacity: 17,942 total bike stands
    o	#1 Lyon, France: 9,350 total stands
    o	#2 Bruxelles-Capitale: 8,592 total stands


o	Location column split into latitude and Longitude columns.
o	Index column is created in fact and dimension tables.
