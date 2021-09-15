# docker-airflow
[![CI status](https://github.com/puckel/docker-airflow/workflows/CI/badge.svg?branch=master)](https://github.com/puckel/docker-airflow/actions?query=workflow%3ACI+branch%3Amaster+event%3Apush)
[![Docker Build status](https://img.shields.io/docker/build/puckel/docker-airflow?style=plastic)](https://hub.docker.com/r/puckel/docker-airflow/tags?ordering=last_updated).

This repository contains **Dockerfile** of [docker-airflow](https://github.com/puckel/docker-airflow) by Puckel and [Airflow tutorial](https://github.com/tuanavu/airflow-tutorial) by Tuan Vu. Puck [automated build](https://registry.hub.docker.com/u/puckel/docker-airflow/). Puckel published to the public [Docker Hub Registry](https://registry.hub.docker.com/).

I added some tweak to the repository considering, that there were some dependencies issues when I tried using the `pandas-gbq` function. I spent sometime researching how to downgrade the dependencies using the Dockerfile. But, I am glad I figured it out.

We wouldn't be pulling the container from docker hub. Instead, we will be building it from this repository. 

## Informations

* Based on Python (3.7-slim-buster) official Image [python:3.7-slim-buster](https://hub.docker.com/_/python/) and uses the official [Postgres](https://hub.docker.com/_/postgres/) as backend and [Redis](https://hub.docker.com/_/redis/) as queue
* Install [Docker](https://www.docker.com/)
* Install [Docker Compose](https://docs.docker.com/compose/install/)
* Following the Airflow release from [Python Package Index](https://pypi.python.org/pypi/apache-airflow)

## Getting started
-   Clone this repo
-   Install Docker, Docker Compose
-   Install and Build docker-airflow-dev:latest

## Build

Installation and build.

    docker build --rm --build-arg AIRFLOW_DEPS="gcp" -t puckel/docker-airflow-dev .


## Usage

By default, docker-airflow runs Airflow with **SequentialExecutor** :

    docker run -d -p 8080:8080 puckel/docker-airflow-dev webserver

If you want to run another executor, use the other docker-compose.yml files provided in this repository.

For **LocalExecutor** :

    docker-compose -f docker-compose-LocalExecutor.yml up -d

For **CeleryExecutor** :

    docker-compose -f docker-compose-CeleryExecutor.yml up -d

NB : If you want to have DAGs example loaded (default=False), you've to set the following environment variable :

`LOAD_EX=n`

    docker run -d -p 8080:8080 -e LOAD_EX=y puckel/docker-airflow-dev

If you want to use Ad hoc query, make sure you've configured connections:
Go to Admin -> Connections and Edit "postgres_default" set this values (equivalent to values in airflow.cfg/docker-compose*.yml) :
- Host : postgres
- Schema : airflow
- Login : airflow
- Password : airflow

## Credits
-   [Apache Airflow](https://github.com/apache/incubator-airflow)
-   [docker-airflow](https://github.com/puckel/docker-airflow)
-   [Airflow tutorial](https://github.com/tuanavu/airflow-tutorial)