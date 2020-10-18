pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..pipeline'
                sh '''#!/bin/bash
                    pwd
                    echo "Hello from bash"
                    echo "Who I'm $SHELL"
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing Pipeline'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....pipeline'
            }
        }
    }
}
