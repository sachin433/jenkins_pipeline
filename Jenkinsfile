pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..pipeline'
                sh '''#!/bin/bash

                    echo "Hello from bash"
                    echo "Who I'm $SHELL"
                '''
            }
        }
        stage('Test') {
            steps {
                ls
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....pipeline'
            }
        }
    }
}
