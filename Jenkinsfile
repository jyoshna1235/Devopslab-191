pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/jyoshna1235/Devopslab-191.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building Project'
            }
        }
        stage('Test') {
            steps {
                echo 'Executing Tests'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deployment Completed'
            }
        }
    }
    post {
        success {
            echo 'Build Successful'
        }
        failure {
            echo 'Build Failed'
        }
        always {
            echo 'Cleaning Workspace'
        }
    }
}
