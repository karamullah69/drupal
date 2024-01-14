pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Build HelloWorld1') {
            steps {
                script {
                    // Create a directory for artifacts
                    sh 'mkdir -p artifacts/helloworld1'

                    // Copy index.html to the artifacts directory
                    sh 'cp HelloWorld1/index.html artifacts/helloworld1/'

                    // Optionally, you can perform additional build steps here
                }
            }
        }

        stage('Build HelloWorld2') {
            steps {
                script {
                    // Create a directory for artifacts
                    sh 'mkdir -p artifacts/helloworld2'

                    // Copy index.html to the artifacts directory
                    sh 'cp HelloWorld2/index.html artifacts/helloworld2/'

                    // Optionally, you can perform additional build steps here
                }
            }
        }

        stage('Deploy to DrupalApp1') {
            steps {
                script {
                    // Create a directory for DrupalApp1 artifacts
                    sh 'mkdir -p DrupalApp1/DrupalApp1'
                    // Copy artifacts to DrupalApp1 directory
                    sh 'cp -r artifacts/helloworld1 DrupalApp1'

                    // Optionally, you can perform additional deployment steps here
                }
            }
        }

        stage('Deploy to DrupalApp2') {
            steps {
                script {
                    // Create a directory for DrupalApp2 artifacts
                    sh 'mkdir -p DrupalApp2/DrupalApp2'
                    // Copy artifacts to DrupalApp2 directory
                    sh 'cp -r artifacts/helloworld2 DrupalApp2/DrupalApp2'

                    // Optionally, you can perform additional deployment steps here
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f DrupalApp1.yaml'
                    sh 'kubectl apply -f DrupalApp2.yaml'
                    // Add deployment steps using kubectl apply
                    // This could involve applying Kubernetes manifests
                    // Make sure your Kubernetes manifests reference the correct paths for the HTML files
                }
            }
        }
    }
}
