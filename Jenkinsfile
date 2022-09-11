pipeline {
  environment {
    registry = "http://ec2-18-212-25-74.compute-1.amazonaws.com:8081/"
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
          sh 'docker build -t flask1:1.0 .'
        }
       }
	  }
    stage('Deploy Image in to nexus registry') {
      steps{
        script {
	   sh 'curl -XGET "admin:pooja" -X PUT http://3.110.86.199:8081/repository/docker-group/flask-app '
           sh 'docker tag flask:1.0 18.212.25.74:8081/repository/k8s-task/flask:1.0'
           //sh 'docker login -u ravali1505 -p Manoj@123@123'
           sh 'docker push 18.212.25.74:8081/repository/k8s-task/flask:1.0'
           sh 'docker logout http://18.212.25.74:8081/repository/k8s-task/'
            }
          }
        }
      }
    }
