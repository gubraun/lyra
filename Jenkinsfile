pipeline {
    agent any
    
    environment {
        ANDROID_NDK_HOME = '/opt/android/sdk/ndk/21.4.7075529'
        ANDROID_HOME = '/opt/android/sdk'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/gubraun/lyra'
            }
        }
        stage('Build') {
            steps {
                sh '/opt/coverity/bin/cov-configure --config coverity_config.xml --gcc'
                sh '/opt/coverity/bin/cov-build --dir idir --bazel bazel build -c opt :coverity-target'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
