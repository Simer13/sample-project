pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('simer13/sample-image', 'app') // Uses Dockerfile in app/
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image('simer13/sample-image').push('latest')
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    def kubeconfigPath = 'C:\\Users\\hp\\.kube\\config'
                    def setKubeEnv = "set KUBECONFIG=${kubeconfigPath} && "

                    bat "${setKubeEnv}kubectl apply -f deployment.yaml"
                }
            }
        }
    }
}
