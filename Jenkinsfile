pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..pipeline'
                whoami
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..pipeline'
                ls
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....pipeline'
                pwd
            }
        }
    }
}
