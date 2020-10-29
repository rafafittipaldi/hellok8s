# hellok8s
Projeto exemplo Docker e Kubernetes

### Comandos básicos Docker (https://docs.docker.com/reference/)
docker build -t (your-image):(your-tag) .  
docker images  
docker ps  
docker rmi -f #image  
docker pull #image  
docker push #image  
docker run -d -p 8181:8181 --name (name-container) (your-image):(your-tag)  
docker stop (container-id)  
docker tag (your-image):(your-tag) (your-image):(new-tag)  
docker exec -it (container-id) /bin/bash  
docker info  
docker context create fittipaldi-server2 --docker "host=tcp://172.21.35.113:2375"  
docker-compose up -d  

### Comandos básicos kubernetes
kubectl config view  
kubectl proxy  
kubectl create deployment (your-deployment) --image=(your-image) --port=8181 --replicas=3 --dry-run=client -o yaml> k8s/deploy.yml  
kubectl create service clusterip (your-service) --tcp=8181 --dry-run=client -o yaml > k8s/service.yml  
kubectl expose deployment (your-deployment) --port=8181 --target-port=8181 --type=LoadBalancer --name=(name-service)  
kubectl apply -f deploy.yml  
kubectl get deployment  
kubectl get deployment -o wide  
kubectl get all  
kubectl get pods  
kubectl describe pods  
kubectl delete pod  
kubectl apply -f service.yml  
kubectl port-forward (your-service) 8181  
kubectl delete all -l app=(your-app)  
kubectl delete (your-service)  
kubectl get services  
kubectl run (your-deployment) --image=(your-image) --replicas=10  
kubectl scale deployment (your-deployment) --replicas=10  
kubectl autoscale deployment (your-deployment) --cpu-percent=50 --min=1 --max=10  

### Reset Builds Jenkins

item = Jenkins.instance.getItemByFullName("hellok8s")  
//THIS WILL REMOVE ALL BUILD HISTORY  
item.builds.each() { build ->  
  build.delete()  
}  
item.updateNextBuildNumber(1)  

### Setup a Jenkins Local DevOps
https://medium.com/@anthony.f.tannous/setup-a-jenkins-local-devops-environment-using-docker-and-wsl2-c74ca47db9be  
https://medium.com/@Joachim8675309/jenkins-environment-using-docker-6a12603ebf9   
https://stackoverflow.com/questions/50916740/docker-command-not-found-in-local-jenkins-multi-branch-pipeline  

### Run commands on remote Docker host
https://gist.github.com/kekru/4e6d49b4290a4eebc7b597c07eaf61f2#enable-docker-remote-api 

### Kubernetes (kubectl) Docker
https://plugins.jenkins.io/kubernetes-cli/   
