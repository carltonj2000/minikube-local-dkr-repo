# Minikube Services

This example is base from the article at the following link.
https://medium.com/techlogs/kubernetes-different-ways-of-exposing-a-service-by-an-example-b81646d20cba

```bash
minikube start
kubectl create namespace test
kubectl delete namespace test
kubectl create deployment nginx2 --image nginx:alpine -n test # deploy
kubectl -n test expose deployment nginx2 --port=80 # service expose
kubectl -n test get svc -o wide
kubectl port-forward service/nginx2 --address 0.0.0.0 8080:80 --namespace test

kubectl patch svc nginx2 -n test -p '{"spec": {"type": "LoadBalancer"}}'
```
