pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker.build('sample-image', 'app')
 .'
                    } else {
                        bat 'docker.build('sample-image', 'app')
 .'
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image('sample-image').push('latest')
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'kubectl apply -f k8s/deployment.yaml'
                    } else {
                        bat 'kubectl apply -f k8s\\deployment.yaml'
                    }
                }
            }
        }
    }
}
