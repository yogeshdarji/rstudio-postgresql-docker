## Dockerizing R and Postgres for PEcAn

Here I have created a dockerfile to install R and R-studio. 

```
#Pull base image
FROM ubuntu:latest

#Update Package and install wget
RUN  apt-get update \
  && apt-get install -y wget \
  && rm -rf /var/lib/apt/lists/*

#Install R
RUN apt-get -y install r-base

#Install R-studio
RUN apt-get install -y gdebi-core
RUN wget https://download2.rstudio.org/rstudio-server-1.0.136-amd64.deb
RUN gdebi rstudio-server-1.0.136-amd64.deb 
```
To link postgres and R-studio, I have created the below docker-compose.yml file

```
version: '2'
services:
  postgres:
    build: .
    links:
      - "db:database"
    db:
      image: postgres
    ports:
     - "5432:5432"
    volumes:
     - ./postgres-volume:/home
    environment:
     - DEBUG=false

     - DB_USER=
     - DB_PASS=
     - DB_NAME=
     - DB_TEMPLATE=

     - DB_EXTENSION=

     - REPLICATION_MODE=
     - REPLICATION_USER=
     - REPLICATION_PASS=
     - REPLICATION_SSLMODE=


  rstudio:
    build: rstudio
    image: rstudio
    volumes:
     - ./rstudio-volume:/home
    environment:
     - env variables
```






