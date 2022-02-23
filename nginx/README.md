# Minikube Nginx

```bash
minikube start
# make sure docker is point to local demon and not minikubes
# simple was to do this a new terminal - no docker envs set

# dev run
docker run --rm -it --name nginx-dev -p 80:80 -v ${PWD}/src:/usr/share/nginx/html:ro nginx:1.21-alpine

# host build and run with docker
docker build -t webserver .
docker run -it --rm -p 80:80 --name web webserver

# minikube build and run with kubectl - some details one level up
eval $(minikube -p minikube docker-env) # point docker cli to minikube
docker build -t carltonj2000/webserver . # build in minikube docker
kubectl create -f deployment.yml
kubectl get pods
kubectl delete -f deployment.yml
kubectl port-forward svc/webserver-service 8080:80 # forward to host
```
