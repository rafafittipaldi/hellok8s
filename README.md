# hellok8s
Projeto exemplo Docker e Kubernetes

### Comandos básicos Docker (https://docs.docker.com/reference/)
docker build -t rafafittipaldi/hellok8s:1.0 .  
docker images  
docker ps  
docker rmi -f #image  
docker pull #image  
docker push #image  
docker run -d -p 8181:8181 rafafittipaldi/hellok8s:1.0  
docker stop #containerid  
docker tag rafafittipaldi/hellok8s:1.0 rafafittipaldi/hellok8s:1.1  
docker exec -it #containerid  
docker info  

### Comandos básicos kubernetes
kubectl create deployment hellok8s --image=rafafittipaldi/hellok8s:1.0 --dry-run -o yaml> deploy.yml  
kubectl apply -f deploy.yml  
kubectl get deploy  
kubectl get deploy -o wide  
kubectl get all  
kubectl create service clusterip hello-svc --tcp=8181 --dry-run -o yaml > service.yml  
kubectl apply -f service.yml  
kubectl port-forward svc/hello-svc 8181  
kubectl delete all -l app=hellok8s  
kubectl delete ing hellok8s  
kubectl delete svc/hello-svc  
