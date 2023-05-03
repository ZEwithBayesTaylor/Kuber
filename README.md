# Docker-Kubernetes

### Overview

The task is to deploy a web application on Kubernetes using Docker containers. Details can be found in this [PDF](/Assignment%203.pdf)

### Workflow

Commands

```bash
# Part 2
docker build -t sy3079/flask-app:latest .
docker-compose up
docker push sy3079/flask-app:latest

# Part 3
minikube start
kubectl apply -f app-depolyment.yaml
minikube service flask-app-service --url

# Part 5
kubectl get pods
kubectl delete pod <pod-name>
# should genereate a new pod
kubectl get pods

# Part 8
# Setup Prometheus monitoring on Kubernetes
# reference: https://devopscube.com/setup-prometheus-monitoring-on-kubernetes/
kubectl create namespace monitoring
kubectl create -f clusterRole.yaml
kubectl create  -f prometheus-deployment.yaml 
kubectl get deployments --namespace=monitoring
kubectl get pods --namespace=monitoring
kubectl port-forward prometheus-monitoring-3331088907-hm5n1 8080:9090 -n monitoring
# reference: https://devopscube.com/setup-kube-state-metrics/
git clone https://github.com/devopscube/kube-state-metrics-configs.git
kubectl apply -f kube-state-metrics-configs/
kubectl get deployments kube-state-metrics -n kube-system
# reference: https://devopscube.com/alert-manager-kubernetes-guide/#
git clone https://github.com/bibinwilson/kubernetes-alert-manager.git
kubectl create -f AlertManagerConfigmap.yaml
kubectl create -f AlertTemplateConfigMap.yaml
kubectl create -f Deployment.yaml
kubectl create -f Service.yaml

minikube service alertmanager --url -n monitoring
```

Some other helpful commands

```bash
# remove all docker images and containers
docker rm $(docker ps -aq)
docker image prune -fa
docker volume prune -f

kubectl get services
minikube dashboard
```
