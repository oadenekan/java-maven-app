# Java Maven Application – CI/CD DevOps Project

## Overview

This project demonstrates a complete **CI/CD pipeline for a Java application** using modern DevOps tools.  
The application is built with Maven, containerized with Docker, and deployed to a Kubernetes cluster through an automated Jenkins pipeline.

The goal of this project is to showcase practical DevOps skills including build automation, containerization, CI/CD pipelines, and Kubernetes deployment.

---

## Tech Stack

- Java
- Apache Maven
- Docker
- Kubernetes
- Jenkins
- GitHub

---

## Architecture

Developer pushes code → GitHub → Jenkins CI Pipeline → Maven Build → Docker Image → Docker Registry → Kubernetes Deployment

Pipeline workflow:

1. Developer pushes code to GitHub
2. Jenkins pipeline triggers automatically
3. Maven builds the Java application
4. Docker image is built and tagged
5. Docker image is pushed to Docker Hub
6. Kubernetes deploys the updated application

---

## Repository Structure
```
java-maven-app
│
├── src/ # Java application source code
├── pom.xml # Maven build configuration
├── Dockerfile # Container image definition
├── Jenkinsfile # CI/CD pipeline configuration
│
├── kubernetes/
│ ├── deployment.yaml # Kubernetes deployment configuration
│ └── service.yaml # Kubernetes service configuration
│
└── README.md
```


---

## CI/CD Pipeline Stages

The Jenkins pipeline performs the following steps:

### 1. Version Increment
Automatically increments the application version using Maven.

### 2. Build Application
Builds the Java application using Maven:
```mvn clean package```


### 3. Build Docker Image
Creates a container image from the application.
```docker build -t olusolaayeni/demo-app:<version> .```


### 4. Push Image to Registry

The image is pushed to Docker Hub for deployment.

### 5. Deploy to Kubernetes

The new image is deployed to the Kubernetes cluster using `kubectl`.

---

## Docker

The application is containerized using Docker.

Build the image:
```docker build -t demo-app .```


Run the container locally:
```docker run -p 8080:8080 demo-app```

---

## Kubernetes Deployment

The application is deployed using Kubernetes manifests.

Deployment file:
```kubernetes/deployment.yaml```

Service file:
```kubernetes/service.yaml```

Deploy to cluster:
```
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml
```

---

## Environment Variables

The deployment uses environment variables for dynamic configuration:

- `APP_NAME`
- `IMAGE_NAME`

These variables are injected during the CI/CD deployment stage.

---

## Skills Demonstrated

This project demonstrates the following DevOps capabilities:

- CI/CD pipeline creation
- containerization with Docker
- Kubernetes application deployment
- automated build and version management
- secure credential management in Jenkins
- infrastructure deployment automation

---

## Future Improvements

Planned enhancements for this project include:

- Infrastructure provisioning using Terraform
- Monitoring with Prometheus
- Visualization with Grafana
- Helm chart deployment
- automated testing integration

---

## Author

**Olu Ayeni**

GitHub: https://github.com/oadenekan
