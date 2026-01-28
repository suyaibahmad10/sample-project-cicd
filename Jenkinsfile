pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git clone https://github.com/suyaibahmad10/sample-project-cicd.git
            }
        }

        stage('Build') {
            steps {
                sh 'echo Building...'
                // add your build commands here, e.g. 'mvn -B -DskipTests package'
            }
        }

        stage('PR-specific') {
            when {
                changeRequest()
            }
            steps {
                echo 'This is a Pull Request build — you can run PR-only checks here.'
            }
        }

        stage('Result') {
            steps {
                bash ./shell_script.sh
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
