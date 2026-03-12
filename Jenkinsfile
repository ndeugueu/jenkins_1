pipeline {
    agent {
        docker {
            image 'node:21-alpine'
        }
    }

    options {
        parallelAlwaysFailFast()
    }

    tools {
        gradle 'gradle'
        Nodejs 'node'
        Docker 'docker'
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

        stage ('build') {
            failFast true
            parallel {
                stage('build frontend') {
            
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

        stage('build backend') {
            
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
            }
        }

        stage ('matrix') {
            matrix {
                axes {
                    axis {
                        name 'PLATEFORM'
                        values 'linux', 'macos', 'windows'
                    }
                    axis {
                        name 'BROWSER'
                        values 'firefox', 'chrome', 'safari'
                    }
                }
                stages {
                    stage('Build') {
                        steps {
                            echo "construire pour ${PLATFORM} - ${BROWSER}"
                        }
                    }
                    stage('Test') {
                        steps {
                            echo "tester pour ${PLATFORM} - ${BROWSER}"
                        }
                    }
                }
            }
        }

        stage ('artefact') {
            steps {
                sh 'echo hello > world.txt'
                archiveArtifacts(artifacts: '*.txt')
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
            emailext (to: 'christianndeugueu@gmail.com', body: 'test body', subject: 'test success')
        }
        failure {
            echo 'failure'
            emailext (to: 'christianndeugueu@gmail.com', body: '$DEFAULT_CONTENT', subject: 't$DEFAULT_SUBJECT')
        }
        always {
            echo 'always'
        }
    }
}