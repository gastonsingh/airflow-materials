# The Complete Hands-On Introduction to Apache Airflow

*Practice of the course:
[The Complete Hands-On Introduction to Apache Airflow](https://www.udemy.com/course/the-complete-hands-on-course-to-master-apache-airflow/).*

## Table of Contents

  1. [Prerequisites](#prerequisites)
  2. [Install Apache Airflow with Docker](#install-apache-airflow-with-docker)
  3. [Install dependencies](#install-dependencies)
  4. [Debug DAG](#debug-dag)

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
```