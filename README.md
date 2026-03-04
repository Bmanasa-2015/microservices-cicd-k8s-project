# Microservices CI/CD K8s Project

## Overview

This project demonstrates an end-to-end CI/CD pipeline using:

* Jenkins
* Docker
* Kubernetes

## CI/CD Flow

Code Push -> Jenkins Build -> Docker Image -> Push to Docker Hub -> Deploy to Kubernetes

## Folder Structure

app/ - Application code \& Dockerfile
k8s/ - Kubernetes manifests
Jenkinsfile - CI/CD pipeline script



