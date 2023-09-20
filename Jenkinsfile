/* Requires the Docker Pipeline plugin */
pipeline {
    agent { docker { image 'golang:1.21.1-alpine3.18' } }
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }
    stages {
        stage('build') {
            steps {
                sh 'go version'
                sh '''
                    echo "The second step is also running"
                    ls -lah
                '''
                echo "Database engine is ${DB_ENGINE}"
                echo "DISABLE_AUTH is ${DISABLE_AUTH}"
                sh 'printenv'
            }
            post {
                always {
                    echo 'This will always run'
                }
                success {
                    echo 'This will run only if successful'
                    mail to: 'kmolha@gmail.com',
                        subject: "Jenkins build was successful",
                        body: "Congrats, old man"
                }
                failure {
                    echo 'This will run only if failed'
                }
                unstable {
                    echo 'This will run only if the run was marked as unstable'
                }
                changed {
                    echo 'This will run only if the state of the Pipeline has changed'
                    echo 'For example, if the Pipeline was previously failing but is now successful'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
            }
        }
        stage('Deploy - Staging') {
            steps {
                echo "Deploying to staging environment"
                echo "Running smoke tests"
            }
        }

        stage('Sanity check') {
            steps {
                mail to: 'kmolha@gmail.com',
                    subject: "Jenkins needs your input",
                    body: "Can you please approve this deployment?"
                input "Does the staging environment look ok?"
            }
        }

        stage('Deploy - Production') {
            steps {
                echo "Deploying to production"
            }
        }
    }
}
