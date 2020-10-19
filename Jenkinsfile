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
                echo myvar
                script { 
                    ls
                    pwd
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....pipeline'
                input message: 'Please pass value', parameters: [string(defaultValue: 'dummy1', description: '', name: 'val1', trim: false)], submitterParameter: 'val1'
            }
        }
        stage('run-parallel-branches') {
          parallel{
            stage('Test On Windows') {
                    steps {
                        echo 'parallel windows execution'
                    }
                    
            }
            stage('Test On Linux') {
                    steps {
                        echo 'parallel Linux execution'
                    }
                    
            }
          }
        }
      }
    
}
