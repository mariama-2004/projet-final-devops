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
                    sh 'docker build -t mon-app-devops .'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -d --name mon-app-devops -p 8081:80 mon-app-devops'
            }
        }

        stage('Monitor') {
            steps {
                sh 'docker ps | grep mon-app-devops'
            }
        }

    }
}
