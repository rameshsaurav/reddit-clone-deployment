# Reddit Clone - Kubernetes Deployment

This repo contains Kubernetes manifests and Docker setup for deploying a Reddit clone React app.

## Prerequisites

Before you begin, you should have the following tools installed on your local machine:

    Docker
    Minikube cluster ( Running )
    kubectl
    Git


## Steps to Deploy

### 1.** Clone this repository and go to project root folder.**

### 2. Login to Docker. Then, Build an Image from Dockerfile by running `docker build -t reddit-clone .` . To verify image, run `docker images`. 

### 3. Push the image to dockerhub by running `docker tag reddit-clone <username>/reddit-clone:latest` & `docker push <username>/reddit-clone:latest`

### 4. Startup minikube and change directory to k8. Next, apply the deployment.yml file by running `kubectl apply -f deployment.yml`. To verify deployment, run `kubectl get deployments`.

### 5. Apply the service.yml file by running `kubectl apply -f service.yml`. To verify, run `kubectl get services`.

### 6. Finally, to access the reddit application running on cluster, run `minikube service reddit-clone-service --url`. It will give you an URL by which you can access the application
