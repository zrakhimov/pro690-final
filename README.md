# Docker Compose

To get started with docker-compose:

`docker compose up -d`

# Test locally with Minikube

`
// Start minikube 
minikube start

// Check minikube dashboard
minikube dashboard

// Create an image from Dockerfile
docker build -t pro690-image . --no-cache

// Create kubectl deployment
kubectl create deployment pro690-app --image=pro690-image:latest
`
