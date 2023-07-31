# 🚀 Welcome to the MERN Stack Web Application - Docker & Kubernetes Deployment Guide 🐳☸️

## Description : 
This project consists of a 3-tier web application developed using the MERN stack (MongoDB, Express, React, Node.js).We use Docker to create containers for the MongoDB database and the frontend and backend parts of the application. Then we  write Dockerfiles for each part and followed best practices for containerization. And using Docker Compose to deploy the entire application and set up a private Docker image registry.

In the second part of the project,we will create Kubernetes manifests to deploy the application in a Kubernetes cluster, set up various probes, and created an Ingress to access the application. we also implemente monitoring and logging using Prometheus, Grafana, and the EFK stack.

## Prerequisites
Before diving into the project, make sure you have the following tools installed:
* Docker
* Kubernetes (e.g., Minikube, MicroK8s)
  
## Part 1: Dockerizing the Application

### 1. MongoDB Containerization
To containerize the MongoDB database, we'll use Docker and make the storage persistent. by executing this command :

```shell
docker run –d --name mongodb-service –v mongo:/data/db –p 27017:27017 mongo:5.0
```
### 2. Docker Network Creation
We'll create a Docker network using an appropriate driver and connect the mongodb-service container to it.
```shell
docker network create –-driver bridge <network_name>
docker network connect <network_name> mongodb-service
```
### 3.Docker Commands for all parts of app 
* Create a Dockerfile for all parts of the application. This file will define the necessary steps to build the backend image:
```shell
docker build -t <image name > .
```
To follow the best practices used in the creation of Dockerfiles, you can refer to this post: : https://www.linkedin.com/posts/asmae-elazrak_docker-devops-dockerimage-activity-7073970892988370944-Kqyk?utm_source=share&utm_medium=member_desktop

* Scan the image for vulnerabilities:
```shell
docker scan  <image name >
```

*  Publish the image to Docker Hub:
```shell
docker login
docker tag <image name> <docker_hub_username>/<image name>:<tag>
docker push <docker_hub_username>/<image name>:<tag>
```
*  Instantiate the image as a local container named backend, sharing the same network with the MongoDB container.:
```shell
docker run -d --name backend --network <network_name> <image name>
```




















Thank you for going through this comprehensive guide for deploying the MERN Stack Web Application using Docker and Kubernetes. We hope you find it helpful! If you encounter any issues or have questions, feel free to reach out or raise an issue in the respective repositories.
Happy Deploying! 😄🚀
