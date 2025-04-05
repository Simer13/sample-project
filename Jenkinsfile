pipeline {
    agent any
stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Simer13/sample-project.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("simer13/sample-app:latest")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'Ravneet@17') {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                kubernetesDeploy configs: 'deployment.yaml', kubeconfigId: 'kubeconfig-id'
            }
        }
    }
}