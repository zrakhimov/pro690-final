# Docker Compose

To get started with docker-compose:

`docker compose up -d`

# Minikube

To get started with Kubernetes cluster using Minikube
Note: the image repository is in my account in dockerhub

```
// Start minikube 
minikube start

// Apply services and deployments
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

// To see it locally, you have to forward port 80 to your desired port on your local machine
kubectl port-forward service/my-service 3000:80

// When you finished, you can cleanup by deleting the service and deployments
kubectl delete service --all
kubectl delete deployment --all      

```

