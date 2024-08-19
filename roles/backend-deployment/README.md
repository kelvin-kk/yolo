# YOLO IP4 ORCHESTRATION WITH KUBERNETES

![image](/images/ip4_homepage.png)

## Requirements

+ Ensure to have an active Google Cloud account with billing enabled
+ Install Google Cloud SDK
+ Install Minikube and Kubectl

### How to install Minikube and Kubectl

#### Installing Minikube
``` 
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube 
 ```

 Checking and confirming installed version
```
minikube version
```

Start Minikube
``` 
minikube start
```

Confirm Minikube is running
```
 minikube status
 ```

#### Installing Kubectl
```
 sudo snap install kubectl --classic
 ```

## Deploying the App

Create manifests directory inside the main project directory 
```
mkdir manifests
```

Create and update the yaml files for each deployment
```
backend-deployment.yaml
client-deployment.yaml
mongodb-deployment.yaml
```

Create the pods 
```
kubectl apply -f backend-deployment.yaml
kubectl apply -f client-deployment.yaml
kubectl apply -f mongodb-deployment.yaml
```

### Kubectl Pods
![image](/images/kubectl_pods.png)

### Kubectl Services
![image](/images/kubectl_services.png)