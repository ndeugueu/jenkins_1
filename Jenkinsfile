pipeline {
    agent {
        docker {
            image 'node:21-alpine'
        }
    }

    //parameters {
    //    string(name: 'NAME', defaultValue: 'nantais', description: 'qui est ce ?')
    //    text(name: 'TEXT', defaultValue: 'un test', description: 'une description')
    //    choice(name: 'CHOICE', choices: ['un', 'deux', 'trois'], description: 'qui est ce ?')
    //}

    triggers {
        //cron('* * * * *')
        pollSCM('* * * * *')
    }

    input {
        
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

        stage('deployement production') {

            input {
                message 'Voulez-vous deployer en prod ?'
                ok 'deployer'
                submitter 'admin,devops'
                submitParameter 'USER_SUBMIT'
                parameters {
                    string(name: 'VERSION', defaultValue: 'latest', description: 'une version')
                }
            }
    
            steps {
                echo "user : ${USER_SUBMIT}"
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