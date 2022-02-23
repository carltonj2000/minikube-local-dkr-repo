# Minikube Local Repository

The `nginx` directory contains details on developing under nginx.

The content of this repository is based on the
[How to Run Locally Built Docker Images in Kubernetes](https://medium.com/swlh/how-to-run-locally-built-docker-images-in-kubernetes-b28fbc32cc1d)
article.

```bash
minikube start
docker build -t carltonj2000/hello-world .
docker run carltonj2000/hello-world
kubectl create -f job.yml
kubectl get pods
# see STATUS of ErrImagePull, due to not in registry
# in job.yml add -> imagePullPolicy: Never
kubectl delete -f job.yml
kubectl create -f job.yml
kubectl get pods
# see STATUS of ErrImageNeverPull, not seen in minikube local registry
minikube docker-env
# point shell's docker cli to minikube's docker-deamon
eval $(minikube -p minikube docker-env)
docker build -t carltonj2000/hello-world . # build in minikube docker
kubectl delete -f job.yml
kubectl create -f job.yml
kubectl get pods
# see STATUS of Completed, not seen in minikube local registry
kubectl logs hello-world--1-gjnbq
```
