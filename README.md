Overview
========

The ETL Weather-Airflow Project! This project demonstrates a complete ETL (Extract, Transform, Load) pipeline using Apache Airflow to fetch, process, and store weather data from the Open-Meteo API into a PostgreSQL database. The project showcases skills in data engineering, ETL pipeline design, and Airflow orchestration.

Project Contents
================

Your Astro project contains the following files and folders:

- dags: This folder contains the Python files for your Airflow DAGs:
    - `etlweather.py`: A custom ETL DAG that extracts current weather data for London from the Open-Meteo API, transforms it, and loads it into PostgreSQL. It uses Airflow hooks for HTTP requests and database connections, demonstrating best practices in data pipeline development.
    - `exampledag.py`: The default example DAG from Astronomer.
- Dockerfile: This file contains a versioned Astro Runtime Docker image that provides a differentiated Airflow experience. If you want to execute other commands or overrides at runtime, specify them here.
- include: This folder contains any additional files that you want to include as part of your project. It is empty by default.
- packages.txt: Install OS-level packages needed for your project by adding them to this file. It is empty by default.
- requirements.txt: Install Python packages needed for your project by adding them to this file. Includes Apache Airflow providers for HTTP and PostgreSQL.
- plugins: Add custom or community plugins for your project to this file. It is empty by default.
- airflow_settings.yaml: Use this local-only file to specify Airflow Connections, Variables, and Pools instead of entering them in the Airflow UI as you develop DAGs in this project.
- Airflow connections.png: Screenshot of Airflow connections configuration.
- Airflow Dag graph view.png: Screenshot of the DAG graph view in Airflow UI.
- Dag running.png: Screenshot of a successful DAG run.
- Database Query results.png: Screenshot of database query results showing inserted weather data.
- Multiple sucessful Dag runs.png: Screenshot of multiple successful DAG runs.

ETL Pipeline Overview
=====================

The `weather_etl_pipeline` DAG performs the following steps:

1. **Extract**: Fetches current weather data (temperature, windspeed, winddirection, weathercode) for London (latitude: 51.5074, longitude: -0.1278) from the Open-Meteo API using the HttpHook.
2. **Transform**: Processes the extracted JSON data into a structured format suitable for database insertion.
3. **Load**: Inserts the transformed data into a PostgreSQL table named `weather_data` using the PostgresHook.

The DAG is scheduled to run daily and uses Airflow connections for API and database credentials.

Prerequisites
=============

- Docker and Docker Compose installed
- Astronomer CLI installed
- Git for version control

Deploy Your Project Locally
===========================

1. Clone the repository and navigate to the project directory.
2. Ensure Docker Desktop is running.
3. Run 'astro dev start' to spin up the Airflow environment.

This command will spin up five Docker containers on your machine, each for a different Airflow component:

- Postgres: Airflow's Metadata Database
- Scheduler: The Airflow component responsible for monitoring and triggering tasks
- DAG Processor: The Airflow component responsible for parsing DAGs
- API Server: The Airflow component responsible for serving the Airflow UI and API
- Triggerer: The Airflow component responsible for triggering deferred tasks

When all five containers are ready the command will open the browser to the Airflow UI at http://localhost:8080/. You should also be able to access your Postgres Database at 'localhost:5432/postgres' with username 'postgres' and password 'postgres'.

Note: If you already have either of the above ports allocated, you can either [stop your existing Docker containers or change the port](https://www.astronomer.io/docs/astro/cli/troubleshoot-locally#ports-are-not-available-for-my-local-airflow-webserver).

Running the ETL Pipeline
=========================

1. Access the Airflow UI at http://localhost:8080/.
2. Enable the `weather_etl_pipeline` DAG.
3. Trigger a manual run or wait for the scheduled execution.
4. Monitor task execution and view logs.
5. Query the `weather_data` table in PostgreSQL to verify data insertion.
=======
Skills Demonstrated
===================

This project showcases proficiency in:

- **Apache Airflow**: DAG creation, task definition using decorators, scheduling, and hook usage.
- **ETL Pipeline Design**: Extracting data from APIs, transforming JSON responses, and loading into databases.
- **Data Engineering**: Handling weather data, database schema design, and error handling.
- **Docker**: Containerization for reproducible environments.
- **PostgreSQL**: Database operations and connection management.
- **Python**: Scripting for data processing and API interactions.
- **Version Control**: Git for project management and collaboration.

Screenshots
===========

![Airflow connections](Airflow%20connections.png "Airflow connections configuration")

![Airflow Dag graph view](Airflow%20Dag%20graph%20view.png "DAG graph view in Airflow UI")

![Dag running](Dag%20running.png "Successful DAG run with all tasks completed")

![Database Query results](Database%20Query%20results.png "Database query results showing inserted weather data")

![Multiple sucessful Dag runs](Multiple%20sucessful%20Dag%20runs.png "Multiple successful DAG runs")
