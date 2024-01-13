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
                    docker.withRegistry('http://0.0.0.0:2375', 'docker-registry-credentials') {
                        docker.image("helloworld1:${env.BUILD_NUMBER}").push()
                        docker.image("helloworld2:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f drupal-app1.yaml'
                    sh 'kubectl apply -f drupal-app2.yaml'
                }
            }
        }
    }
}
