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
kubectl config view
kubectl proxy
kubectl create deployment hellok8s --image=rafafittipaldi/hellok8s:1.0 --dry-run -o yaml> deploy.yml  
kubectl apply -f deploy.yml  
kubectl get deploy  
kubectl get deploy -o wide  
kubectl get all  
kubectl get pods 
kubectl describe pods
kubectl delete pod
kubectl create service clusterip hello-svc --tcp=8181 --dry-run -o yaml > service.yml  
kubectl apply -f service.yml  
kubectl port-forward svc/hello-svc 8181  
kubectl delete all -l app=hellok8s  
kubectl delete ing hellok8s  
kubectl delete svc/hello-svc  
kubectl get services  

### Setup a Jenkins Local DevOps
https://medium.com/@anthony.f.tannous/setup-a-jenkins-local-devops-environment-using-docker-and-wsl2-c74ca47db9be 
https://medium.com/@Joachim8675309/jenkins-environment-using-docker-6a12603ebf9   
https://stackoverflow.com/questions/50916740/docker-command-not-found-in-local-jenkins-multi-branch-pipeline  

### Run commands on remote Docker host
https://gist.github.com/kekru/4e6d49b4290a4eebc7b597c07eaf61f2#enable-docker-remote-api  
