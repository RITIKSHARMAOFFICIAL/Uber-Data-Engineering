# Uber-Data_Engineering

![uber_logo](https://github.com/enochiankim/NYC-uber-data-engineering-project-etl-pipeline/blob/main/uber-logo-map.jpeg)

## Introduction

The objective of this project is to analyze Uber trip data using a variety of tools and technologies, including Google Cloud Platform (GCP) Storage, Python, Compute Engine, Mage Data Pipeline Tool, BigQuery, and Looker Studio. The analysis aims to answer the following key questions:

1. What are the top 10 pickup locations ranked by the number of trips?
2. How many trips have been made based on passenger count?
3. How does the average fare amount vary across different hours of the day?

[![Project Overview Video](https://img.youtube.com/vi/1l8XJf3SRFz5yllOvogaYqQUa6l-pLKZ8/0.jpg)](https://drive.google.com/file/d/1l8XJf3SRFz5yllOvogaYqQUa6l-pLKZ8/view?usp=drive_link)

## Dataset Used

**TLC Trip Record Data**

The dataset includes trip records for yellow and green taxis, with fields such as pickup and drop-off dates/times, locations, distances, itemized fares, rate types, payment methods, and driver-reported passenger counts.

- [Dataset Link](https://github.com/enochiankim/NYC-uber-data-engineering-project-etl-pipeline/tree/main/uber_raw_data)
- [Website](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)
- [Data Dictionary](https://www.nyc.gov/assets/tlc/downloads/pdf/data_dictionary_trip_records_yellow.pdf)

## Utilized Technologies

**Programming Language**: Python

**Google Cloud Platform Components**:
1. Google Storage
2. Compute Engine
3. BigQuery
4. Looker Studio

**Data Pipeline Tool**:
- Mage - [Mage](https://www.mage.ai)

## Project Steps

### Step 1: Developing the Architectural Framework
<img src="project_architecture.jpg" alt="Project Architecture">

### Step 2: Data Modeling and Entity-Relationship Diagram
<img src="Uber_data_model.PNG" alt="Uber Data Model">

### Step 3: Developing the Transformation Code using Python
- [Transformation Code](https://github.com/enochiankim/NYC-uber-data-engineering-project-etl-pipeline/blob/main/Uber%20Data%20Pipeline.ipynb)

### Step 4: Creating a GCP Project and Bucket
- Upload the data to the bucket, set up the server, and configure necessary permissions.
<img src="google_cloud.PNG" alt="Google Cloud Setup">

### Step 5: Generating a Virtual Machine Instance in GCP
Commands to set up the VM:
```
sudo apt-get install update
sudo apt-get install python3-distutils
sudo apt-get install python3-apt
sudo apt-get install wget
wget https://bootstrap.pypa.io/get-pip.py
sudo python3 get-pip.py
```

### Step 6: Connecting VM to Mage Project and Setting Up Dependencies
<img src="mage.PNG" alt="Mage Setup">

### Step 7: Constructing a Data Pipeline with Mage
- Use Mage blocks such as data loader, transformer, and exporters. Integrate your transformation code into the data transformer.
<img src="etl_flow.PNG" alt="ETL Flow">
- [ETL Pipeline Code](https://github.com/enochiankim/NYC-uber-data-engineering-project-etl-pipeline/tree/main/etl_pipelines)

### Step 8: Configuring GCP Credentials
- Include GCP credentials in the `io_config.yaml` configuration file.

### Step 9: Using BigQuery for Data Querying and ETL Operations
<img src="bigquery.PNG" alt="BigQuery Setup">

### Step 10: Developing a Dashboard in Looker Studio
- Build dashboards to visualize insights. Alternatives like Power BI or Tableau can also be used.
<img src="Looker_Dashboard.PNG" alt="Looker Studio Dashboard">

## SQL Queries and Results

### Top 10 Pickup Locations
```sql
SELECT pickup_location_id, count(pickup_location_id) AS Trip_Num
FROM `uber_data_engineering_yt.fact_table`
GROUP BY pickup_location_id
ORDER BY Trip_Num DESC
LIMIT 10;
```
<img src="Q3.PNG" alt="Top 10 Pickup Locations">

### Trips by Passenger Count
```sql
SELECT passenger_count, count(passenger_count) AS passenger_trip
FROM `uber_data_engineering_yt.tbl_analytics`
GROUP BY passenger_count
ORDER BY passenger_trip DESC;
```
<img src="Q2.PNG" alt="Trips by Passenger Count">

### Average Fare Amount by Hour
```sql
SELECT d.pick_hour, ROUND(AVG(fare_amount), 2) AS fare
FROM `uber_data_engineering_yt.fact_table` f
JOIN `uber_data_engineering_yt.datetime_dim` d ON f.datetime_id = d.datetime_id
GROUP BY d.pick_hour
ORDER BY fare DESC;
```
<img src="Q1.PNG" alt="Average Fare Amount by Hour">

This project provides a comprehensive experience in handling large datasets, performing ETL (Extract, Transform, Load) processes, and creating impactful data visualizations using industry-standard tools and platforms.
