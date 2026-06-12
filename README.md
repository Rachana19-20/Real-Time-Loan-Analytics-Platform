# Real-Time Loan Analytics Platform

## Overview

The Real-Time Loan Analytics Platform is a streaming analytics solution that enables financial institutions to monitor loan performance in real time. The platform uses Apache Kafka for event streaming, MySQL for data storage, and Streamlit for interactive dashboards.

The system continuously processes loan events such as approvals, rejections, repayments, and pending applications, providing instant insights into loan portfolios, borrower behavior, and operational performance.

---

## Features

* Real-time loan event streaming using Apache Kafka
* Automated data ingestion and processing
* MySQL-based data storage
* Interactive Streamlit dashboard
* Live KPI monitoring
* Loan approval and rejection analytics
* Real-time trend analysis
* Searchable loan records
* Auto-refresh dashboard updates
* Docker support for deployment

---

## Tech Stack

### Backend

* Python
* Apache Kafka
* MySQL

### Frontend & Visualization

* Streamlit
* Matplotlib
* Pandas

### Supporting Libraries

* kafka-python
* mysql-connector-python
* ConfigParser
* Logging
* JSON

---


## Prerequisites

### Hardware Requirements

* Processor: Intel Core i3 or above
* RAM: Minimum 8 GB
* Storage: 20 GB Free Space
* Stable Internet Connection

### Software Requirements

* Python 3.10 or 3.11
* Apache Kafka 3.0+
* Zookeeper
* MySQL 8.0+
* Streamlit
* Git (Optional)
* Docker (Optional)

---

# Database Setup

### Step 1: Create Database

```sql
CREATE DATABASE loan_data;
USE loan_data;
```

### Step 2: Create Loan Events Table

```sql
CREATE TABLE loan_events (
    loan_id CHAR(36) NOT NULL,
    user_id CHAR(36) NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    status ENUM('pending','approved','rejected','closed') DEFAULT 'pending',
    timestamp BIGINT NOT NULL,
    PRIMARY KEY (loan_id)
);
```

### Step 3: Configure Database Connection

Update:

```bash
config/config.ini
```

```ini
[mysql]
host = localhost
user = root
password = your_password
database = loan_data
```

### Step 4: Test Connection

```bash
python test_mysql_connection.py
```

Expected Output:

```bash
Connection Successful!
Database: loan_data
Table: loan_events
```

---

# Installation

### Clone Repository

```bash
git clone <repository-url>
cd Real_Time_Loan_Analytics_Platform
```

### Create Virtual Environment

#### Windows

```bash
py -3.10 -m venv venv_streamlit
venv_streamlit\Scripts\activate
```

#### Linux/Mac

```bash
python3.10 -m venv venv_streamlit
source venv_streamlit/bin/activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

Or manually:

```bash
pip install streamlit
pip install pandas
pip install matplotlib
pip install kafka-python
pip install mysql-connector-python
pip install numpy
pip install plotly
pip install streamlit-autorefresh
```

---

# Running the Project Locally

## 1. Start Zookeeper

```bash
cd C:\kafka

.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
```

## 2. Start Kafka Broker

```bash
cd C:\kafka

.\bin\windows\kafka-server-start.bat .\config\server.properties
```

## 3. Create Kafka Topic

```bash
.\bin\windows\kafka-topics.bat --create \
--topic loans \
--bootstrap-server localhost:9092
```

---

## 4. Start Kafka Consumer

```bash
python kafka_consumer.py
```

---

## 5. Start Loan Event Producer

```bash
python produce_test_events.py
```

This generates sample loan events and streams them into Kafka.

---

## 6. Launch Streamlit Dashboard

```bash
streamlit run loan_dashboard.py
```

Dashboard URL:

```bash
http://localhost:8501
```

The dashboard automatically refreshes and displays live loan analytics.

---

## Dashboard Metrics

The platform provides:

* Total Loans Processed
* Total Loan Amount
* Approved Loans
* Pending Loans
* Approval Rate
* Average Loan Amount
* Loan Amount by Status
* Loan Count by Status
* Average Loan Trend
* Top Borrowers
* Detailed Loan Records

---

## Docker Deployment (Optional)

Start all services:

```bash
docker-compose up
```

Stop services:

```bash
docker-compose down
```

---

## Workflow

```text
Loan Events
      │
      ▼
Kafka Producer
      │
      ▼
Kafka Topic (loans)
      │
      ▼
Kafka Consumer
      │
      ▼
MySQL Database
      │
      ▼
Streamlit Dashboard
      │
      ▼
Real-Time Loan Analytics
```

---

## Future Enhancements

* Loan Risk Prediction
* Fraud Detection
* Borrower Credit Scoring
* AWS/GCP Deployment
* Role-Based Access Control
* Power BI Integration
* Alerting & Notification System



A scalable real-time financial analytics solution built using Kafka, MySQL, Python, and Streamlit for monitoring and analyzing loan performance with low-latency insights.
