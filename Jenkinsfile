pipeline {
  agent any
  stages {
    stage('Initial cleanup') {
      steps {
        dir(path: "${WORKSPACE}") {
          deleteDir()
        }

      }
    }

    stage('Cloning Git') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/dybran/Project-20.git']]])
      }
    }

    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build registry
        }

      }
    }

    stage('Pushing to ECR') {
      steps {
        script {
          sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 939895954199.dkr.ecr.us-east-1.amazonaws.com'
          sh 'docker push 939895954199.dkr.ecr.us-east-1.amazonaws.com/tooling-ecr-repo-b4b7b5bt'
        }

      }
    }

    stage('Clean Up') {
      steps {
        cleanWs(cleanWhenAborted: true, cleanWhenNotBuilt: true, cleanWhenUnstable: true, cleanWhenFailure: true)
      }
    }

  }
  environment {
    registry = '939895954199.dkr.ecr.us-east-1.amazonaws.com/tooling-ecr-repo-b4b7b5b'
  }
}