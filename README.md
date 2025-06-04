# 🚀 Real-Time SCD Pipeline with Apache NiFi, AWS & Snowflake

## 🧩 Overview
This project demonstrates a real-time data ingestion and transformation pipeline that supports **Slowly Changing Dimensions (SCD)** using **Snowflake Streams and Tasks**. It simulates continuous user data, processes it through cloud-native tools, and manages both current and historical records within Snowflake.

---

## 🏗️ Architecture
![SCD Architecture](https://github.com/HaseebWar/HaseebWar-Streaming-Data-Ingestion-Pipeline-AWS-NiFi-Snowflake/blob/main/notes/images/SCD_Architecture.png)

---

## ⚙️ Tech Stack
- **Languages:** Python 3, SQL, JavaScript  
- **Services/Tools:** Apache NiFi, Amazon EC2, Amazon S3, Docker, Snowflake

---

## 📊 Dataset Description
User data is synthetically generated using the Python faker library. Files are saved as CSVs with timestamps. Each record includes:
- customer_id
- first_name
- last_name
- email
- street
- state
- country

---

## 🔄 Data Pipeline Workflow

1. **Data Generation (EC2):**  
   Python script running on EC2 generates and stores synthetic CSV files locally.

2. **File Transfer (Apache NiFi):**  
   NiFi monitors the local directory and uploads new files to an AWS S3 bucket.

3. **Data Ingestion (Snowpipe):**  
   Snowpipe auto-loads the data from S3 into a Snowflake staging table.

4. **CDC and Transformation (Snowflake):**
   - A Snowflake Task triggers a stored procedure every minute.
   - A MERGE command applies insert/update/delete logic to the main table (CDC).
   - Staging table is truncated after processing.

5. **Historical Tracking (Streams + SCD):**  
   - Snowflake Stream captures changes made to the target table.
   - Type 1 and Type 2 SCD logic is applied to populate a historical table.

---

## 🎯 Key Learning Outcomes

- Understanding SCD concepts and types
- Building a complete real-time data pipeline
- Managing AWS EC2 instances and security
- Containerizing services with Docker and docker-compose
- Working with Apache NiFi for file and flow management
- Configuring Snowflake components: Snowpipe, Stream, Task, Stored Procedures
- Implementing both **SCD Type 1** and **Type 2**

---

## ✅ Benefits

- **Near Real-Time Data Processing:** Quickly reflects changes in Snowflake
- **CDC Implementation:** Ensures target data stays current and accurate
- **Historical Data Integrity:** Tracks and stores record history using SCD techniques
- **Cloud-Native Scalability:** Easily adaptable for larger workloads using AWS and Snowflake

---

## 📚 FAQs

### ❓ What are Slowly Changing Dimensions (SCD)?
In data warehousing, **facts** represent measurable data (e.g., sales), and **dimensions** provide context (e.g., customer, product). SCDs manage changes in dimension attributes over time to preserve historical context.

**Common SCD Types:**
- **Type 0:** Passive; original data remains unchanged.
- **Type 1:** Overwrites old data with new; no history maintained.
- **Type 2:** Keeps full history; closes old record and inserts a new one.
- **Type 3:** Keeps current and one previous value in separate columns.

---

### 🛠️ Tool Highlights

#### Apache NiFi
A data flow orchestration tool used for real-time movement of data between systems.

#### Docker
Containerization platform that packages software and dependencies for consistent deployment.

#### Amazon EC2
Elastic cloud computing service for scalable virtual servers.

#### Amazon S3
Object storage service used to store and retrieve any volume of data from anywhere.

#### Snowflake
Cloud-based data warehouse supporting SQL analytics, real-time ingestion, and complex transformations using:
- **Warehouse**
- **Database/Schema**
- **Table & View**
- **Stored Procedure**
- **Snowpipe**
- **Stream**
- **Task**

---

## 📌 Summary
This project provides a complete example of building a real-time, cloud-native data pipeline from scratch, with strong emphasis on **data warehousing best practices** and **change data capture techniques** using Snowflake.
