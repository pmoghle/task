pipeline {
  environment {
    registry = "http://18.212.25.74:8081/repository/k8s-task/"
    registryCredential = 'nexus'
    }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/ganigapetaravali/task.git'
      }
    }
  }
}
