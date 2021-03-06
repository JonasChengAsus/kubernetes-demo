# Cheet Sheet


## Deploy Containers

```shell
kubectl create deployment first-deployment --image=katacoda/docker-http-server
kubectl expose deployment first-deployment --port=80 --type=NodePort
export PORT=$(kubectl get svc first-deployment -o go-template='{{range.spec.ports}}{{if .nodePort}}{{.nodePort}}{{"\n"}}{{end}}{{end}}')
curl http://localhost:$PORT
# remove resources
kubectl delete services first-deployment
kubectl delete deployment first-deployment
```

## Deploy Containers Using YAML

```shell
cat deployment.yaml
kubectl create -f deployment.yaml
kubectl describe deployment deployment-webapp
cat service.yaml
kubectl create -f service.yaml
kubectl describe service svc-webapp
curl http://localhost:30080
# remove resources
kubectl delete services svc-webapp
kubectl delete deployment deployment-webapp
```

## Deploy Containers on Selected Nodes

```shell
kubectl label node docker-desktop node=master
cat deployment-master-node.yaml
kubectl create -f deployment-master-node.yaml
cat deployment-other-node.yaml
kubectl create -f deployment-other-node.yaml
# there should be one pending pod
kubectl get pods
# remove resources
kubectl delete deployment deployment-webapp-master
kubectl delete deployment deployment-webapp-other
```
