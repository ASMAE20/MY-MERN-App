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
docker build -t <image name> .
```
To follow the best practices used in the creation of Dockerfiles, you can refer to this post: : https://www.linkedin.com/posts/asmae-elazrak_docker-devops-dockerimage-activity-7073970892988370944-Kqyk?utm_source=share&utm_medium=member_desktop

* Scan the image for vulnerabilities:
```shell
docker scan  <container name>
```

*  Publish the image to Docker Hub:
```shell
docker login
docker tag <image name> <docker_hub_username>/<image name>:<tag>
docker push <docker_hub_username>/<image name>:<tag>
```
*  Instantiate the image as a local container, sharing the same network with the MongoDB container:
```shell
docker run -d --name <container name> --network <network_name> <image name>
```
*  Inspect the container:
```shell
docker inspect <container name>
```
*  Display logs related to the container:
```shell
docker logs <container name>
```
### 4.Docker Compose file

Instead of executing all these commands, you can simply apply the Docker Compose file by using the command :
```shell
docker compose up
```
Please remember that 'docker-compose-app' uses an image from a private registry, while the 'docker-compose' file uses an image from a public repository.

##  Part 2: Kubernetes Deployment
All the necessary Kubernetes YAML files (manifests) to deploy the application within a Kubernetes cluster under the namespace 'exam' can be applied by using the following command:

```shell
kubectl apply -f <path_to_yaml_files_directory>
```
For the directory called "k8s-file" located in the current working directory . The command to apply those files to the Kubernetes cluster under the 'exam' namespace would be:
```shell
kubectl apply -f k8s-file
```
You can verify the application pods and services are running:
```shell
kubectl get all -n=exam
```
##  Accessing the Application 🌐

Open your browser and access the application using: http://asmae-k8s.com

##  Monitoring and Logging

* Prometheus and Grafana are set up for monitoring. Access Grafana dashboard at http://localhost:9070.

* The EFK stack is used for logging. Access Kibana dashboard at http://localhost:5601.

🎉 Congratulations! You now have the fully containerized MERN stack application running in Kubernetes, monitored, and logged effectively. Enjoy exploring and developing further! 😊

🔍 For more in-depth information about each task and detailed steps, please refer to the project repository and the provided code in the respective directories.

Thank you for going through this comprehensive guide for deploying the MERN Stack Web Application using Docker and Kubernetes. We hope you find it helpful! If you encounter any issues or have questions, feel free to reach out or raise an issue in the respective repositories.

Happy Deploying! 😄🚀
