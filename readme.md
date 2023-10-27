# Loan Eligibility Model Monitoring using Airflow and Docker

## Project Overview

### Objective

This project focuses on creating an end-to-end pipeline for model and drift monitoring, ensuring that a loan eligibility classification model remains accurate over time.

---

### Practical Application

In real-world scenarios, machine learning models deployed in production may encounter data drift, concept drift, or model degradation. Monitoring these changes is essential to maintain the model's effectiveness. By orchestrating monitoring pipelines with Airflow and Docker, this project demonstrates practical solutions for real-time model and data tracking.

---

### Data Description

The project retrieves data from a PostgreSQL server related to loan eligibility. The dataset may contain various features and labels that influence loan decisions. Participants will work with this real-world data to build, monitor, and evaluate a machine learning model.

---

### Tech Stack

- Language: `Python`
- Libraries: `pandas`, `numpy`, `matplotlib`, `scikit-learn`, `deepchecks`, `sqlalchemy`, `psycopg2-binary`
- Services: `Airflow`, `Docker`, `PostgreSQL`

---

### Approach

The project follows a structured approach:

1. Extracting data from PostgreSQL.
2. Data preprocessing, including train-test splitting, encoding, imputation, rescaling, and feature engineering.
3. Building and evaluating machine learning models (Random Forest and Gradient Boosting).
4. Monitoring for concept drift, data drift, and model drift.
5. Orchestrating monitoring pipelines using Airflow.

---

### Data Privacy and Security

This project considers data privacy and security, especially when dealing with sensitive information related to loan eligibility. It emphasizes best practices for handling and protecting such data.

---

### Error Handling

The project includes robust error handling and data validation mechanisms to ensure the quality and reliability of the monitoring process.

---

### Deployment Considerations

The project discusses deployment considerations for monitoring systems in a production environment. It covers best practices and potential challenges in deploying machine learning models and monitoring solutions.

---

### Key Concepts Explored

1. Skills to connect Python to a PostgreSQL server.
2. Understanding of conditional data extraction.
3. Proficiency in missing value imputation, data rescaling, and feature engineering.
4. Knowledge of monitoring concept drift, data drift, and model drift.
5. Experience in deploying and orchestrating monitoring pipelines with Airflow and Docker.

---

### Note: This project requires the data to be present in postgres server.

The data is available in code>main>dags>data>raw location.

Kindly upload the data and provide the appropriate credentials in code>main>dags>creds.json file.

## 1. ML pipeline monitoring using?

- Deepcheks
- Airflow
- Slack integration: alerts

---

## 2. Environment Setup

Here we will simply setup our environment using docker.

1. Make sure [docker](https://docs.docker.com/get-started/) and [docker-compose](https://docs.docker.com/get-started/08_using_compose/) are setup properly
2. Make a github repo an check in all the code which can be found [here](https://s3.amazonaws.com/projex.dezyre.com/ml-model-monitoring-using-apache-airflow-and-docker/materials/code.zip).
3. Clone the gitrepo: `git clone git@github.com:your git address`
4. To proceed, make sure

   - Docker can have access to at least 4GB of Memory on your system
   - Navigate to `dags/src/config.py` and ensure `RUN_LOCAL` is set to `False`
5. While in the same home directory as `docker-compose.py` start docker-compose by issuing this command on you terminal: `docker-compose up`
   This will take a couple of minutes to boot up all containers. To check if all containers are running properly, you can run `docker ps --all`. You should see a list of all containers in `healthy` status

   ```
      CONTAINER ID   IMAGE                   COMMAND                  CREATED         STATUS                    PORTS                               NAMES
      5dea90526ec4   apache/airflow:2.2.4    "/usr/bin/dumb-init …"   23 hours ago    Up 23 hours (healthy)     8080/tcp                            project_01_model-testing_airflow-scheduler_1
      b27cf17c76d4   apache/airflow:2.2.4    "/usr/bin/dumb-init …"   23 hours ago    Up 23 hours (healthy)     8080/tcp                            project_01_model-testing_airflow-triggerer_1
      b254faa326cb   apache/airflow:2.2.4    "/usr/bin/dumb-init …"   23 hours ago    Up 23 hours (healthy)     0.0.0.0:5555->5555/tcp, 8080/tcp    project_01_model-testing_flower_1
      79af795c2ab2   apache/airflow:2.2.4    "/usr/bin/dumb-init …"   23 hours ago    Up 23 hours (healthy)     8080/tcp                            project_01_model-testing_airflow-worker_1
      cfe8d1b18f77   apache/airflow:2.2.4    "/usr/bin/dumb-init …"   23 hours ago    Up 23 hours (healthy)     0.0.0.0:8080->8080/tcp              project_01_model-testing_airflow-webserver_1
      c68fc80dbf0d   postgres:13             "docker-entrypoint.s…"   23 hours ago    Up 23 hours (healthy)     5432/tcp                            project_01_model-testing_postgres_1
      5c0b9f136b75   redis:latest            "docker-entrypoint.s…"   23 hours ago    Up 23 hours (healthy)     6379/tcp                            project_01_model-testing_redis_1
   ```

---

## 3. How to reset environments

1. Delete all files under the following subdirectories. In case subdirectories do not exist (due to .gitignore) please create them

   - `dags/data/raw/*`
   - `dags/data/preprocessed`
   - `dags/models`
   - `dags/results`

   At the end, the directory should be structured as following (ensure to manually create any directory that is missing)

   ```
       ├── airflow.sh
       ├── dags
       │   ├── app.py
       │   ├── credentials.json
       │   ├── dag_pipeline.py
       │   ├── dag_training.py
       │   ├── data
       │   │   ├── preprocessed
       │   │   │   ├── 
       │   │   └── raw
       │   │       ├── 
       │   ├── main.py
       │   ├── models
       │   │   ├── deploy_report.json
       │   ├── results
       │   │   ├── 
       │   ├── src
       │   │   ├── config.py
       │   │   ├── drifts.py
       │   │   ├── etl.py
       │   │   ├── helpers.py
       │   │   ├── inference.py
       │   │   ├── preprocess.py
       │   │   ├── queries.py
       │   │   └── train.py
       ├── docker-compose.yaml
       ├── jobs
       ├── logs
       │   ├── 
       ├── plugins
       ├── readme.md
       └── requirements.txt
   ```
2. Truncate the `mljob` table

   - `truncate mljob;`

---

## Monitoring Machine Learning Pipeline

### 1. Traditional machine learning model training pipeline

1. data gathering
2. data preprocessing
3. model training
4. model evaluation
5. model serving

### 2. The idea behind model training monitoring

1. data integrity
2. data drift
3. concept drift
4. comparative analysis of models

---
