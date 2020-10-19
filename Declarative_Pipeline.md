//Documentattion for pipeline syntax can be found at:

${YOUR_JENKINS_URL}/pipeline-syntax

//to build another job

build 'my-first-pro'

//to print pwd

pwd()

//To write a shell script

sh '''ls
pwd'''

//To run arbitrary pipeline "groovy" script

script {
    // some block
}

//To checkout from git

checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/sachin433/jenkins_pipeline.git']]])

OR

git branch: 'main', url: 'https://github.com/sachin433/jenkins_pipeline.git'

//To echo a message

echo 'trying out groovy script'

//To run a command in particular container(of Jenkins slave pod)

container('my-container') {
    // some block
}

//To pass interactive input:(meant to stop further execution of pipeline.we can't  echo this parameter)

input message: 'Please pass value', parameters: [string(defaultValue: 'Dummy', description: '', name: 'val1', trim: false)]

//To print variable in pipeline

echo userInput

//Parallel execution in pipeline

A) SCRIPTED WAY

 parallel firstBranch: {
        // do something
    }, secondBranch: {
        // do something else
    }

B) DECLARATIVE WAY:

stage('Run Tests') {
            parallel {
                stage('Test On Windows') {
                    agent {
                        label "windows"
                    }
                    steps {
                        echo 'on windows'
                    }
                    }
                stage('Test On Linux') {
                    agent {
                        label "linux"
                    }
                    steps {
                        echo 'on linux'
                    }
                    }
            }
        }


