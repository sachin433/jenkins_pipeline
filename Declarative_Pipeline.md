//Documentattion for pipeline syntax can be found at:
${YOUR_JENKINS_URL}/pipeline-syntax

//to build another job
build 'my-first-pro'

//to print pwd
pwd()

//To run arbitrary pipeline script
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
