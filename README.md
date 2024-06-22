# Uber-Data_Engineering

![uber-logo-map](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/cabfdccf-03be-47ef-b818-4ab7afd19d40)


## Introduction

The objective of this project is to analyze Uber trip data using a variety of tools and technologies, including Google Cloud Platform (GCP) Storage, Python, Compute Engine, Mage Data Pipeline Tool, BigQuery, and Looker Studio. The analysis aims to answer the following key questions:

1. What are the top 10 pickup locations ranked by the number of trips?
2. How many trips have been made based on passenger count?
3. How does the average fare amount vary across different hours of the day?



## Dataset Used

**TLC Trip Record Data**

The dataset includes trip records for yellow and green taxis, with fields such as pickup and drop-off dates/times, locations, distances, itemized fares, rate types, payment methods, and driver-reported passenger counts.

- [Dataset Link] (https://drive.google.com/file/d/1c3qXz2Ir38ZHGps_QuwouxOMtKZP1tZJ/view?usp=drive_link)
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
![project_architecture (1)](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/e63f0a9b-1cdf-4ebe-a783-3bbd5949834f)


### Step 2: Data Modeling and Entity-Relationship Diagram
![Uber Data Model](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/d7334767-4772-4f30-8723-8c94dd5d54c5)


### Step 3: Develop the Transformation Code using Python

### Step 4: Creating a GCP Project and Bucket
- Upload the data to the bucket, set up the server, and configure necessary permissions.
![google_cloud](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/dec1453d-d18b-45e9-b501-26444b13b590)


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
![google_cloud](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/14687850-33ab-4168-8145-d973744e34e6)


### Step 7: Constructing a Data Pipeline with Mage
- Use Mage blocks such as data loader, transformer, and exporters. Integrate your transformation code into the data transformer.
![google_cloud](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/f3e6f9c9-afdb-4cd5-bc81-7496ab6949ee)


### Step 8: Configuring GCP Credentials
- Include GCP credentials in the `io_config.yaml` configuration file.

### Step 9: Using BigQuery for Data Querying and ETL Operations
![PNG](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/cfc4033b-d3b2-421b-a5ce-78e2f8619faf)


### Step 10: Developing a Dashboard in Looker Studio
- Build dashboards to visualize insights. Alternatives like Power BI or Tableau can also be used.
![Screenshot 2024-06-22 162928](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/09ccbd83-0aab-460b-b800-6a5415365b01)
![Screenshot 2024-06-22 163148](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/65217af3-04e1-46c5-847c-d9d73cb8500e)
![Screenshot 2024-06-22 163116](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/c02f5897-2263-4bac-a087-c1c0b03e3d40)




## SQL Queries and Results

### Top 10 Pickup Locations
```SQL
SELECT pickup_location_id, count(pickup_location_id) AS Trip_Num
FROM `uber_data_engineering_yt.fact_table`
GROUP BY pickup_location_id
ORDER BY Trip_Num DESC
LIMIT 10;
```
![Q1](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/7eacf3a0-2325-48b2-b44e-9cafceef664c)


### Trips by Passenger Count
```SQL
SELECT passenger_count, count(passenger_count) AS passenger_trip
FROM `uber_data_engineering_yt.tbl_analytics`
GROUP BY passenger_count
ORDER BY passenger_trip DESC;
```
![Q2](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/2f298589-9e27-43dc-99de-71d3d0f14aba)


### Average Fare Amount by Hour
```SQL
SELECT d.pick_hour, ROUND(AVG(fare_amount), 2) AS fare
FROM `uber_data_engineering_yt.fact_table` f
JOIN `uber_data_engineering_yt.datetime_dim` d ON f.datetime_id = d.datetime_id
GROUP BY d.pick_hour
ORDER BY fare DESC;
```
![Q3](https://github.com/RITIKSHARMAOFFICIAL/Uber-Data-Engineering/assets/96929769/840a3f96-9792-4b08-949b-76114e57c163)

This project provides comprehensive experience in handling large datasets, performing ETL (Extract, Transform, Load) processes, and creating impactful data visualizations using industry-standard tools and platforms.
