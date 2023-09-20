/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'golang:1.21.1-alpine3.18' } }
    stages {
        stage('build') {
            steps {
                sh 'go version'
                sh '''
                    echo "The second step is also running"
                    ls -lah
                '''
            }
        }
    }
}
