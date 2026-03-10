pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "BRANCH_NAME : ${ env.BRANCH_NAME }"
                echo "BRANCH_IS_PRIMARY : ${ env.BRANCH_IS_PRIMARY  }"

            }
        }
    }
}