# Amazon Data ETL Pipeline with Apache Airflow & Docker

![ETL Pipeline Diagram](An_infographic_diagram_illustrates_an_ETL_(Extract.png)

## Table of Contents
1. [Project Overview](#project-overview)
2. [Architecture Diagram](#architecture-diagram)
3. [Prerequisites](#prerequisites)
4. [Setup & Installation](#setup--installation)
5. [Configuration](#configuration)
6. [Usage](#usage)
7. [Airflow DAGs](#airflow-dags)
   - [fetch_and_store_amazon_books](#fetch_and_store_amazon_books)
8. [Directory Structure](#directory-structure)
9. [Troubleshooting](#troubleshooting)
10. [Contributing](#contributing)
11. [License](#license)

---

## Project Overview
A Dockerized ETL pipeline using Apache Airflow to scrape book data from Amazon, transform it, and load into a PostgreSQL database.

## Architecture Diagram
![ETL Pipeline Diagram](An_infographic_diagram_illustrates_an_ETL_(Extract.png)

## Prerequisites
- Docker Desktop (with Linux containers)
- Docker Compose v2
- Python 3.8+
- (Optional) Virtual environment for local ETL script testing

## Setup & Installation
1. Clone the repo.  
2. Copy `.env.example` → `.env` and adjust `AIRFLOW_UID` if needed.  
3. Start containers:
   ```bash
   docker compose up --build -d
Configuration
Airflow: adjust docker-compose.yaml under x-airflow-common.

Postgres: connection in Airflow UI → Host: postgres, Port: 5432, Login/Password/DB: airflow.

pgAdmin: http://localhost:5050, default credentials from compose env.

Usage
Browse Airflow UI at http://localhost:8080

Enable & trigger the fetch_and_store_amazon_books DAG.

Monitor logs via:


docker compose logs -f airflow-scheduler
Airflow DAGs
fetch_and_store_amazon_books
fetch_book_data: PythonOperator fetches book details and pushes to XCom.

create_table: PostgresOperator creates the books table.

insert_book_data: PythonOperator reads from XCom and inserts rows into Postgres.

Directory Structure
bash
Copy
Edit
├── dags/
│   └── app.py              # Airflow DAG definition
├── logs/
├── plugins/
├── config/
│   └── airflow.cfg
├── env/             # Python virtual environment
├── etl.py                  # Standalone ETL script for local testin
├── docker-compose.yaml
├── README.md
└── .env

Troubleshooting
Version warning: remove legacy version: attribute from compose file if prompted.

Provider import errors: ensure _PIP_ADDITIONAL_REQUIREMENTS: apache-airflow-providers-postgres.

Connection refused: verify Docker containers are running and hostnames (postgres, localhost) match your connection settings.

Contributing
Fork and clone.

Create a topic branch.

Submit a PR with tests & documentation updates.

License
Apache 2.0 ©+
