pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build and Push Docker Image') {
            steps {
                script {
                    docker.build("helloworld1:${env.BUILD_NUMBER}")
                    docker.build("helloworld2:${env.BUILD_NUMBER}")
                    docker.withRegistry('https://your-docker-registry/', 'docker-registry-credentials') {
                        docker.image("helloworld1:${env.BUILD_NUMBER}").push()
                        docker.image("helloworld2:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    kubernetesDeploy(
                        kubeconfigId: 'your-kubeconfig-credentials',
                        configs: 'drupal-app1.yaml'
                    )
                    kubernetesDeploy(
                        kubeconfigId: 'your-kubeconfig-credentials',
                        configs: 'drupal-app2.yaml'
                    )
                }
            }
        }
    }
}
