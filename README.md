# 🚀 Welcome to the MERN Stack Web Application - Docker & Kubernetes Deployment Guide 🐳☸️

## Description : 
This project consists of a 3-tier web application developed using the MERN stack (MongoDB, Express, React, Node.js).We use Docker to create containers for the MongoDB database and the frontend and backend parts of the application. Then we  write Dockerfiles for each part and followed best practices for containerization. And using Docker Compose to deploy the entire application and set up a private Docker image registry.

In the second part of the project,we will create Kubernetes manifests to deploy the application in a Kubernetes cluster, set up various probes, and created an Ingress to access the application. we also implemente monitoring and logging using Prometheus, Grafana, and the EFK stack.

## Part 1: Dockerizing the Application

### 1. MongoDB Containerization
To containerize the MongoDB database, we'll use Docker and make the storage persistent. by executing this command :

```shell
docker run –d --name mongodb-service –v mongo:/data/db –p 27017:27017 mongo:5.0
```

