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
        stage('Coverity Build') {
            steps {
                sh '/opt/coverity/bin/cov-configure --config coverity_config.xml --gcc'
                sh '/opt/coverity/bin/cov-build --config coverity_config.xml --dir idir --bazel bazel build -c opt :coverity-target'
            }
        }
        stage('Coverity Analysis') {
            steps {
                sh '/opt/coverity/bin/cov-analyze --config coverity_config.xml --dir idir --strip-path $(bazel info execution_root 2>/dev/null)'
            }
        }
        stage('Save Build') {
            steps {
                sh '/opt/coverity/bin/cov-manage-emit --dir idir export-json-build --output-file lyra-full.json --strip-path $(bazel info execution_root 2>/dev/null)'
                archiveArtifacts artifacts: 'lyra-full.json', followSymlinks: false
            }
        }
    }
}
