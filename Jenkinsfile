pipeline {
    
    agent any
    
    tools {
        maven "M3"
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
        
        stage ('Docker build, push') {
            steps {
                // This step should not normally be used in your script. Consult the inline help for details.
                withDockerRegistry(credentialsId: 'f39c2138-3ef3-47fd-b7b1-35de793c7711', url: 'https://index.docker.io/v1/') {
                    sh 'docker build -t ${ImageName}:${BUILD_NUMBER} .'
                    sh 'docker push ${ImageName}'
                }
            }
        }
        
        stage ('Deploy kubernetes, publish') {
            steps {
                sh 'kubectl create deployment hellok8s --image=${ImageName}:${BUILD_NUMBER} --dry-run -o yaml > k8s/deploy.yml'
                sh 'kubectl apply -f k8s/deploy.yml'
                sh 'kubectl apply -f k8s/service.yml'
                sh 'kubectl port-forward svc/hello-svc 8181'
            }
        }
    }
}