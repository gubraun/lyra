pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/gubraun/lyra'
            }
        }
        stage('Build') {
            steps {
                sh ' bazel build -c opt :encoder_main'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
