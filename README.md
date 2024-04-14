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


# Argo CD


### Step 1
UI way - 
https://argo-cd.readthedocs.io/en/stable/getting_started/#creating-apps-via-ui

CLI way -
```
kubectl config set-context --current --namespace=argocd

argocd app create pro690-app  \
--repo https://github.com/zrakhimov/pro690-final.git \
--path k8s \
--dest-server https://kubernetes.default.svc \
--dest-namespace default

kubectl config set-context --current --namespace=default


```


### Step 2
```
// When you finished, you can cleanup by deleting the service and deployments
kubectl delete service --all
kubectl delete deployment --all
kubectl delete rollout --all
kubectl delete application --all 
```

# Argo Rollouts

### See rollout status
```
kubectl argo rollouts get rollout my-rollout --watch
```
### Updating image
```
kubectl argo rollouts set image my-rollout \
  my-rollout=zrakhimov/pro690-image:v2
```
Once the weight reaches 20% it pauses and needs to be continued manually. It's set in the rollout.yaml file

### Promote rollout

```
kubectl argo rollouts promote my-rollout

```
