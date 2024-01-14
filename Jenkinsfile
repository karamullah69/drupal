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
                    // Deploy Drupal applications
                    kubernetesDeploy(
                        kubeconfigId: 'your-kubeconfig',
                        configs: 'drupal-app1.yaml,drupal-app2.yaml',
                        enableConfigSubstitution: true,
                        secretName: 'your-k8s-secret'
                    )

                    // Copy HTML file to Drupal pod
                    kubernetesExec(
                        kubeconfigId: 'your-kubeconfig',
                        podName: 'drupal-app1-6695984fbc-wwv8h', // Update with the actual pod name
                        containerName: 'drupal',
                        command: ['cp', '/var/www/html/hello-world.html', '/var/www/html/sites/default/']
                    )

                    kubernetesExec(
                        kubeconfigId: 'your-kubeconfig',
                        podName: 'drupal-app2-7ff667b74-kh5nz', // Update with the actual pod name
                        containerName: 'drupal',
                        command: ['cp', '/var/www/html/hello-world.html', '/var/www/html/sites/default/']
                    )
                }
            }
        }
    }
}
