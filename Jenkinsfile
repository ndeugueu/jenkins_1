pipeline {
    agent {
        docker {
            image 'node:21-alpine'
        }
    }


    stages {
        stage('build') {
            options {
                timestamps()
            }
            steps {
                sh 'npm -v'

            }
        }
    }

    post {
        success {
            echo 'success'
        }

        failure {
            echo 'failure'
        }

        always {
            echo 'always'
        }
    }
}