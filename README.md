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

### Step 1 
```
kubectl create namespace argo-rollouts
kubectl apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
```


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


# Azure Kubernetes Cluster (AKS)

### Create Cluster

I called it `my-cluster` in azure.

### Login

```
az login
```

### Connect AKS in local env

You'd need to have Azure CLI and kubectl installed.
```
az aks get-credentials --name my-cluster --resource-group pro690-resource-group
/// Merged "my-cluster" as current context in /Users/zokir/.kube/config
```

Basically at this point i have 2 contexts. First one is in my local machine called "**minikube**"
Second is called "**my-cluster**" which is AKS
To get the list of contexts run:
```
 kubectl config get-contexts
```
To switch contexts:

```
kubectl config use-context my-cluster

```


### Login to Docker hub

Needed to pull the image when yaml is applied.
```
docker login -u zrakhimkov
````


## Create application

**Pre-req:**
Make sure to create argo cd (step 1) and argo rollout (step 1) namespaces and installations

### Step 1
You need to login to argo cd

```
argocd login localhost:8080
```

### Step 2
Create the app
```
argocd app create pro690-app  \              
--repo https://github.com/zrakhimov/pro690-final.git \
--path k8s \
--dest-server https://kubernetes.default.svc \
--dest-namespace default

```

application 'pro690-app' created

### Step 3

See it in the UI (localhost:8080 )
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
![Screenshot at Apr 14 15-37-06](https://github.com/zrakhimov/pro690-final/assets/22464933/8a672464-36a8-4aa5-b26b-4ef55437e538)





