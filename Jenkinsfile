pipeline {
    agent any
    stages {
        stage('Nettoyage') {
            steps {
                sh 'docker rm -f mon-app-devops || true'
            }
        }
        stage('Build Docker Image') {
            steps {
                dir('/home/mariama/mon-projet-devops') {
                    sh 'docker build -t mon-app-devops:latest .'
                }
            }
        }
        stage('Deploy Container') {
            steps {
                sh 'docker run -d --name mon-app-devops -p 8081:80 mon-app-devops:latest || true'
            }
        }
        stage('Deploy Kubernetes') {
            steps {
                sh 'minikube image load mon-app-devops:latest'
                sh 'kubectl rollout restart deployment mon-app-devops'
                sh 'kubectl get pods'
            }
        }
        stage('Monitor') {
            steps {
                sh 'kubectl top pods || true'
                sh 'docker ps | grep mon-app-devops'
            }
        }
    }
}
