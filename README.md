# 🕸️ Web Scraping + Data Lake Project

A robust and scalable data engineering pipeline for extracting, processing, and storing web data in a cloud-based data lake. This project simulates an end-to-end pipeline for collecting product information from e-commerce websites and storing it in a well-organized and queryable data lake on AWS S3. The project includes scraping, data cleansing, metadata management, partitioning, and orchestration.

---

## 🔍 Objective

Build a production-grade data pipeline that scrapes data from target web sources, transforms it into a structured format, and stores it in a scalable cloud data lake architecture. The goal is to create a foundation for analytics and business intelligence workloads.

---

## ⚙️ Tech Stack

| Layer              | Tool/Service                      |
|-------------------|------------------------------------|
| Web Scraping       | Python, BeautifulSoup, Requests, Selenium (optional) |
| Data Transformation| Pandas, PyArrow                   |
| Cloud Storage      | AWS S3 (Data Lake)                |
| Orchestration      | Apache Airflow                    |
| Metadata Catalog   | AWS Glue Catalog                  |
| Query Layer        | AWS Athena                        |
| Monitoring         | CloudWatch, Logging (JSON format) |

---

## 🧱 Project Architecture

```plaintext
          +---------------------+
          |  Web Scraper (Python)|
          +----------+----------+
                     |
                     v
          +----------+----------+
          | Transformation Layer|
          | (clean, dedup, enrich) |
          +----------+----------+
                     |
                     v
          +----------+----------+
          | Data Lake (S3)      |
          | Partitioned by date |
          +----------+----------+
                     |
                     v
          +----------+----------+
          | AWS Glue Catalog    |
          +----------+----------+
                     |
                     v
          +----------+----------+
          | Query Layer (Athena)|
          +---------------------+
```

---

## 📦 Folder Structure

```
web-scraping-datalake/
│
├── dags/                      # Airflow DAGs
│   └── etl_scrape_pipeline.py
├── scraper/
│   ├── scraper.py             # Scraping logic
│   └── utils.py               # Helper functions
├── transformer/
│   └── transform.py           # Data cleaning, formatting
├── data/                      # Local data storage (for testing)
├── configs/
│   └── settings.yaml          # Configurations for sites, headers, proxies
├── logs/
│   └── etl_logs.json          # Structured logging
├── s3_bucket_structure.md     # Description of S3 layout
├── requirements.txt
└── README.md
```

---

## 🧪 Key Features

- ✅ Modular scraping pipeline for multiple websites  
- ✅ Daily batch ingestion using Apache Airflow  
- ✅ Schema consistency and version control  
- ✅ Partitioned Parquet storage in S3 (e.g., `s3://datalake/ecommerce/products/dt=2025-05-06/`)  
- ✅ Queryable via AWS Athena with Glue Table integration  
- ✅ Fault-tolerant with retry logic and error alerting  
- ✅ Monitoring and structured logging  

---

## 🚀 Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/param-2003/web-scraping-datalake.git
cd web-scraping-datalake
```

### 2. Install Dependencies
```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 3. Configure AWS
Ensure your AWS CLI is configured with access to S3 and Glue.
```bash
aws configure
```

### 4. Create S3 Buckets
Update your `settings.yaml` with your S3 bucket name and prefix.

### 5. Run Scraper Locally
```bash
python scraper/scraper.py --site "example_site"
```

### 6. Trigger via Airflow
Place the DAG in your Airflow `dags/` directory and trigger it manually or via scheduler.

---

## 🧹 Sample Output Format (Parquet Schema)

```parquet
product_id: string
title: string
price: float
currency: string
availability: string
scraped_date: date
source_url: string
```

---

## 📊 Querying with Athena

You can query structured data using Athena:
```sql
SELECT title, price, availability
FROM ecommerce_products
WHERE dt = '2025-05-06';
```

---

## 📈 Future Improvements

- Add support for real-time scraping with Kafka  
- Integrate data quality checks using Great Expectations  
- Add Change Data Capture (CDC) features  
- Visual dashboard using Looker Studio or Tableau  
- Include proxy rotation and CAPTCHA solving support  

---


## 📄 License

MIT License – see the LICENSE file for details.
