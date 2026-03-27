# Delhivery Operational Data Analysis (Industry: Logistics)
Delhivery, India’s largest fully integrated logistics provider, aims to build an intelligent operating system for commerce. This project focuses on transforming raw, fragmented trip-level data into structured, analysis-ready features to optimize routing, forecasting, and strategic decision-making

# Project Overview
This project examines Delhivery's operational data, which contains complex multi-row trip records, segment-level routing, and time-distance metrics. The analysis involves extensive data cleaning, multi-level aggregation (sub-journey and trip levels), and feature engineering to evaluate network efficiency and operational bottlenecks.

# Problem Statement
The challenge is to convert massive volumes of raw logistics data into reliable features. Specifically, the project addresses:
  * Cleaning and sanitizing fragmented data with missing values and outliers.
  * Merging multi-row entries into unified trip-level records.
  * Validating the relationship between actual operational metrics and OSRM (Open Source Routing Machine) predictions.

# Objectives
 * Clean and Structure Data: Handle missing values in center names and remove outliers using the Interquartile Range (IQR) method.
 * Feature Engineering: Extract city, state, and place information from center names and decompose timestamps into day, week, month, and hour.
 * Hypothesis Testing: Statistically compare actual travel times and distances against OSRM estimates to identify discrepancies.
 * Identify Operational Patterns: Determine the busiest routes, states, and peak times for order bookings .

# Data Set
 * data - tells whether the data is testing or training data
 * trip_creation_time – Timestamp of trip creation
 * route_schedule_uuid – Unique Id for a particular route schedule
 * route_type – Transportation type
 * FTL – Full Truck Load: FTL shipments get to the destination sooner, as the truck is making no other pickups or drop-offs along the way
 * Carting: Handling system consisting of small vehicles (carts)
 * trip_uuid - Unique ID given to a particular trip (A trip may include different source and destination centers)
 * source_center - Source ID of trip origin
 * source_name - Source Name of trip origin
 * destination_cente – Destination ID
 * destination_name – Destination Name
 * od_start_time – Trip start time
 * od_end_time – Trip end time
 * start_scan_to_end_scan – Time taken to deliver from source to destination
 * is_cutoff – Unknown field
 * cutoff_factor – Unknown field
 * cutoff_timestamp – Unknown field
 * actual_distance_to_destination – Distance in Kms between source and destination warehouse
 * actual_time – Actual time taken to complete the delivery (Cumulative)
 * osrm_time – An open-source routing engine time calculator which computes the shortest path between points in a given map (Includes usual traffic, distance through major and minor roads) and gives the time (Cumulative)
 * osrm_distance – An open-source routing engine which computes the shortest path between points in a given map (Includes usual traffic, distance through major and minor roads) (Cumulative)
 * factor – Unknown field
 * segment_actual_time – This is a segment time. Time taken by the subset of the package delivery
 * segment_osrm_time – This is the OSRM segment time. Time taken by the subset of the package delivery
 * segment_osrm_distance – This is the OSRM distance. Distance covered by subset of the package delivery
 * segment_factor – Unknown field

# Milestones
 * Data Exploration: Initial shape analysis (144,867 rows, 24 columns) and null detection.
 * Sub-Journey Aggregation: Merging segments into "mini-trips" based on trip_uuid, source, and destination.
 * Trip-Level Aggregation: Final consolidation of data at the unique trip_uuid level.
 * Feature Creation: deriving od_time_diff_mins, state/city names, and temporal components.
 * Outlier Treatment: Identifying and removing outliers in numeric fields like actual_time and osrm_distance.
 * Statistical Analysis: Performing t-tests to compare actual vs. OSRM metrics.
 * Data Standardization: One-hot encoding route_type and scaling numeric features using StandardScaler.

# Findings
 * Missing Values: source_name (293 nulls) and destination_name (261 nulls) did not impact analysis due to available center IDs.
 * Route Type: The dataset is dominated by Carting (8,816 trips) compared to FTL (3,928 trips).
 * Distribution: All numeric columns are right-skewed and contained significant outliers prior to treatment.
 * Operational Discrepancy:
     * There is no significant difference between start_scan_to_end_scan and od_time_diff_mins.
     * There is a significant difference between actual_time and osrm_time (p-value ≈ 0), indicating OSRM predictions often deviate from reality.
 * Geographic Insights:
     * Maharashtra is the state with the highest order volume (2,309), followed by Karnataka.
     * Bengaluru, Gurgaon, and Mumbai are the top contributor cities.
     * 86.67% of orders are intra-state (within the same state).
 * Peak Timing: Wednesday is the busiest day for bookings, followed by Saturday.

# Recommendations
 * Optimize Routing Engines: Revisit the configuration of the routing engine (OSRM) as there is a significant gap between predicted and actual travel times.
 * Resource Allocation: Prioritize ground resources and infrastructure in Maharashtra and Karnataka, as these states generate the heaviest traffic.
 * Market Expansion: Investigate and increase presence in Central, Eastern, and North-Eastern zones, where order volumes are currently low.
 * Data Standardization: Consolidate city naming conventions (e.g., merging "Mumbai", "Mumbai Hub", and "Lower Parel") to ensure accurate city-level ranking and analytics.
 * Targeted Campaigns: Launch marketing advertisements in states with low engagement like Arunachal Pradesh, Nagaland, and Himachal Pradesh.

# Colab Link 
 * https://colab.research.google.com/drive/1WAeWJUC-K85NKPGz15bdM8F-BLwIKvfg

# Data Link
 * https://drive.google.com/file/d/1hLSdtN2KYtdXfLF6-RxiXHSA5uu2TaOK/view?usp=drive_link
