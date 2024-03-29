# The Complete Hands-On Introduction to Apache Airflow

*Practice of the course:
[The Complete Hands-On Introduction to Apache Airflow](https://www.udemy.com/course/the-complete-hands-on-course-to-master-apache-airflow/).*

## Table of Contents

  1. [Prerequisites](#prerequisites)
  2. [Install Apache Airflow with Docker](#install-apache-airflow-with-docker)
  3. [Install dependencies](#install-dependencies)
  4. [Create Connections](#create-connections)
  5. [Debug DAG](#debug-dag)

## Prerequisites

1. Download [Docker](https://docs.docker.com/get-docker/).
2. Download [PyCharm Community Edition
](https://www.jetbrains.com/pycharm/) or [Visual Studio Code](https://code.visualstudio.com/download).

Docker needs privilege rights to work, make sure you have them. If you have troubles to install these tools, here are some videos to help you

- [Install Docker on Windows 10](https://www.youtube.com/watch?v=lIkxbE_We1I&ab_channel=JamesStormes)
- [Install Docker on Windows 10 with WSL 2](https://www.youtube.com/watch?v=h0Lwtcje-Jo&ab_channel=BeachcastsProgrammingVideos)
- [Install Docker on Windows 11](https://youtu.be/6k1CyA5zYgg?t=249)

## Install Apache Airflow with Docker

1. Open your terminal or CMD and go into [airflow-materials]()

2. Create [.env](.env) with:
```dotenv
AIRFLOW_IMAGE_NAME=apache/airflow:2.4.2
AIRFLOW_UID=50000
```

3. In terminal run:
```bash
docker-compose up -d
```

4. Open AirFlow in the browser: [localhost:8080](http://localhost:8080)
```text
Username: airflow
Password: airflow
```

## Install dependencies

1. [Apache Airflow](https://airflow.apache.org/)
```bash
pip install apache-airflow
```

2. [Apache AirFlow Providers Postgres](https://airflow.apache.org/docs/apache-airflow-providers-postgres/stable/index.html)
```bash
pip install apache-airflow-providers-postgres
```

3. [pandas](https://pandas.pydata.org/)
```bash
pip install pandas 
```

## Create Connections

1. Postgres
```text
Connection Id: postgres
Connection Type: Postgres
Host: postgres
Login: airflow
Password: airflow
Port: 5432
```

2. HTTP
```text
Connection Id: user_api
Connection Type: HTTP
Host: https://randomuser.me/
Login: airflow
Password: airflow
```

## Debug DAG
List your docker containers
```bash
docker-compose ps
```
Access to the scheduler bash
```bash
docker exec -it airflow-materials-airflow-scheduler-1 /bin/bash
```
Check the commands and execute task test
```bash
airflow -h
airflow tasks test user_processing create_table
airflow tasks test user_processing extract_user 2022-01-01
airflow tasks test user_processing process_user 2022-01-01
```
Access to the worker
```bash
docker exec -it airflow-materials-airflow-worker-1 /bin/bash
```
Check worker files
```bash
ls /tmp
```
Access to the postgres sql
```bash
docker exec -it airflow-materials-postgres-1 /bin/bash 
```
Enter into psql
```bash
psql -Uairflow
```
Then show the data into users table
```sql
SELECT * FROM users;
```

### Section 6: Databases and Executors
```bash
docker cp airflow-materials-airflow-scheduler-1:/opt/airflow/airflow.cfg .
```
```bash
docker-compose down
```
```bash
docker-compose up -d
```

### Section 8: Creating Airflow Plugins with Elasticsearch and PostgreSQL
```bash
docker compose -f docker-compose-es.yaml up -d
```
```bash
docker compose -f docker-compose-es.yaml ps
```
```bash
docker exec -it airflowmaterials-airflow-scheduler-1 /bin/bash
```
```bash
curl -X GET 'http://elastic:9200'
```

3. Elastic
```text
Connection Id: elastic_default
Connection Type: HTTP
Host: elastic
Port: 9200
```

Restart docker to add ElasticHook
```bash
docker-compose -f docker-compose-es.yaml stop
```
```bash
docker compose -f docker-compose-es.yaml up -d
```
```bash
docker exec -it airflowmaterials-airflow-scheduler-1 /bin/bash
```
```bash
airflow plugins
```
