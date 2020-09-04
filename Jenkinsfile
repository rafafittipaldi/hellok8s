pipeline {
    
    agent any
    
    tools {
        maven "M3"
    }
    
    environment {
        ci_image_name = "rafafittipaldi/hellok8s:${BUILD_NUMBER}"
    }
    
    stages {
        stage ('Build') {
            steps {
                git 'http://172.21.35.113:3000/rafafittipaldi/hellok8s.git'
                sh ' pwd && ls '
                sh 'mvn -Dmaven.test.failure.ignore=true clean package'
            }
            
            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        
        stage ('Docker build, publish Docker Hub') {
            steps {
                sh 'echo Imagem: ${ci_image_name}'
                // This step should not normally be used in your script. Consult the inline help for details.
                withDockerRegistry(credentialsId: 'b600e99d-1e2e-43dd-b404-121da7318f6a', url: 'https://index.docker.io/v1/') {
                    sh 'docker build -t ${ci_image_name} .'
                    sh 'docker push ${ci_image_name}'
                }
            }
        }
        
        
        
        stage ('Deploy kubernetes, publish') {
            steps {
                withKubeConfig(credentialsId: 'file-kube', serverUrl: 'https://kubernetes.docker.internal:6443') {
                    sh 'kubectl delete all -l app=hellok8s'
                    sh 'rm k8s/deploy.yml'
                    sh 'kubectl create deployment hellok8s --image=${ci_image_name} --dry-run -o yaml > k8s/deploy.yml'
                    sh 'kubectl apply -f k8s/deploy.yml'
                    //sh 'kubectl apply -f k8s/service.yml'
                    
                    sleep(time: 10, unit: "SECONDS")
                    
                    sh 'kubectl expose deployment hellok8s --port=8181 --target-port=8181 --type=LoadBalancer --name=hello-svc'
                }
            }
        }
    }
}