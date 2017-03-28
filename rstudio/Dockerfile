# Pull base image
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
