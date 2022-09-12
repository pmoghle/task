pipeline {
  environment {
    registry = "http://ec2-18-212-25-74.compute-1.amazonaws.com:8081/"
    registryCredential = 'nexus'
    dockerImage = ''	  
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
          sh 'docker build -t flask:1.0 .'
        }
       }
	  }
    stage('Deploy Image in to nexus registry') {
      steps{
        script {
	   sh 'curl "admin:ravali" -X PUT http://18.212.25.74:8081/repository/k8s-task/flask:1.0 '
		//flask:1.0.push("latest")
          // sh 'docker tag flask:1.0 18.212.25.74:8081/repository/k8s-task/flask:1.0'
           //sh 'docker login -u ravali1505 -p Manoj@123@123'
           //sh 'docker push 18.212.25.74:8081/repository/k8s-task/flask:1.0'
          // sh 'docker logout http://18.212.25.74:8081/repository/k8s-task/'
            }
          }
        }
      }
    }
