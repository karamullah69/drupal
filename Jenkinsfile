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
            // Copy artifacts to DrupalApp1 directory
            sh 'cp -r artifacts/helloworld1 /path/to/drupalapp1'

            // Optionally, you can perform additional deployment steps here
        }
    }
}

stage('Deploy to DrupalApp2') {
    steps {
        script {
            // Copy artifacts to DrupalApp2 directory
            sh 'cp -r artifacts/helloworld2 /path/to/drupalapp2'

            // Optionally, you can perform additional deployment steps here
        }
    }
}
