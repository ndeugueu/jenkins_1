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
        string(name: 'VERSION', defaultValue: 'latest', description: 'une version')
        booleanParam(name: 'DEPLOY_TO', defaultValue: false description: 'production')
    }

    triggers {
        pollSCM('* * * * *')
    }

    environment {
        DEPLOY_TO = 'production'
    }

    stages {
        stage('build') {
            options {
                timestamps()
            }
            when {
                allof {
                    branch 'prod'
                    equals expected: true, actual: params.DEPLOY_TO
                }
                
            }
            steps {
                sh 'npm -v'
                echo "NAME: ${params.NAME}"
                echo "CHOICE: ${params.CHOICE}"
            }
        }

        stage('deployement production') {
            input {
                message 'Voulez-vous deployer en prod ?'
                ok 'deployer'
                submitter 'admin,devops'
                submitterParameter 'USER_SUBMIT'
            }

            steps {
                echo "user : ${USER_SUBMIT}"
                echo "version : ${VERSION}"
                echo "deploy"
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