pipeline {
    agent {
        docker {
            image 'node:21-alpine'
        }
    }

    parameters {
        string(name: 'NAME', defaultValue: 'nantais', description: 'qui est ce ?')
        text(name: 'TEXT', defaultValue: 'un test', description: 'une description')
        choice(name: 'CHOICE', choices: ['un', 'deux', 'trois'], description: 'qui est ce ?')
    }


    stages {
        stage('build') {
            options {
                timestamps()
            }
            steps {
                sh 'npm -v'
                echo "NAME: ${NAME}"
                echo "CHOICE: ${CHOICE}"

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