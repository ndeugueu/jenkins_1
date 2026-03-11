pipeline {
    agent any

    stages {
        stage('build') {
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