pipeline {
    agent any
    
    environment {
        ANDROID_NDK_HOME = '/home/gunnar/android/sdk/ndk/21.4.7075529'
        ANDROID_HOME = '/home/gunnar/android/sdk'
    }

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
