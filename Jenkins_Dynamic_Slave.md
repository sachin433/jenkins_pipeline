Jenkins slaves can be defined in pipeline and then used.However default execution always goes to the jnlp container.

A]SCRIPTED PIPELINE

//This will run in jnlp container

podTemplate {
    node(POD_LABEL) {
        stage('Run shell') {
            sh 'echo hello world'
        }
    }
}


//This will be container specific

podTemplate(containers: […]) {
  node(POD_LABEL) {
    stage('Run shell') {
      container('mycontainer') {
        sh 'echo hello world'
      }
    }
  }
}

==================================================================================================================================================================================
//Multiple containers can be defined for the agent pod, with shared resources, like mounts. Ports in each container can be accessed as in any Kubernetes pod, by using localhost.

The container statement allows to execute commands directly into each container.

podTemplate(containers: [
    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'golang', image: 'golang:1.8.0', ttyEnabled: true, command: 'cat')
  ]) {

    node(POD_LABEL) {
        stage('Get a Maven project') {
            git 'https://github.com/jenkinsci/kubernetes-plugin.git'
            container('maven') {
                stage('Build a Maven project') {
                    //sh 'mvn -B clean install'
                    echo 'executing mvn project'
                }
            }
        }

        stage('Get a Golang project') {
            git url: 'https://github.com/hashicorp/terraform.git'
            container('golang') {
                stage('Build a Go project') {
                      echo 'executing goland project'
                }
            }
        }

    }
}



================================================================================================================================================================================

B] DECLARATIVE PIPELINE:
------------------------
pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: maven
    image: maven:alpine
    command:
    - cat
    tty: true
  - name: busybox
    image: busybox
    command:
    - cat
    tty: true
"""
    }
  }
  stages {
    stage('Run maven') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
        container('busybox') {
          sh '/bin/busybox'
        }
      }
    }
  }
}


===============================================

we can even pass yaml file as below to keep the pod template in a separate KubernetesPod.yaml file

pipeline {
  agent {
    kubernetes {
      yamlFile 'KubernetesPod.yaml'
    }
  }
  stages {
      ...
  }
}


========================================================================================================

Key Point: Unlike scripted k8s template, declarative templates do not inherit from parent template.




