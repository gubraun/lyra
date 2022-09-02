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
        stage('Coverity') {
            steps {
                sh '/opt/coverity/bin/cov-configure --config coverity_config.xml --gcc'
                sh '/opt/coverity/bin/cov-build --dir idir --bazel bazel build -c opt :coverity-target'
                sh '/opt/coverity/bin/cov-analyze --dir idir --strip-path $(bazel info execution_root 2>/dev/null)'
            }
        }
        stage('Save Build') {
            steps {
                sh '/opt/coverity/bin/cov-manage-im --dir idir export-json-build --output-file lyra-full.json'
                archiveArtifacts artifacts: 'lyra-full.json', followSymlinks: false
            }
        }
    }
}
