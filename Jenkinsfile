pipeline {
  environment {
    registry = "http://18.212.25.74:8081/repository/k8s-task/"
    registryCredential = 'nexus'
    }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git branch: 'main', url: 'https://github.com/ganigapetaravali/task.git'
      }
    }
   stage('Building image') {
      steps{
        script {
          sh 'docker build -t flask:1.0 -f Dockerfile'
        }
      }
    }
    stage('Deploy Image in to nexus registry') {
      steps{
        script {
           sh 'docker tag http://18.212.25.74:8081/repository/k8s-task/flask:1.0'
           sh 'docker login -u admin -p ravali http://18.212.25.74:8081/repository/k8s-task/'
           sh 'docker push http://18.212.25.74:8081/repository/k8s-task/flask:1.0'
           sh 'docker logout http://18.212.25.74:8081/repository/k8s-task/'
            }
          }
        }
      }
    }
    //stage('Remove Unused docker image') {
      //steps{
        //sh "docker rmi $registry:$BUILD_NUMBER"
    }
  }
}
  }
}
