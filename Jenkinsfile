pipeline {
  environment {
    registry = "18.212.25.74:8001/repository/k8s-task/"
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
          sh 'docker build -t flask:5.0 .'
        }
       }
	  }
    stage('Deploy Image in to nexus registry') {
      steps{
        script {
	   //sh 'curl "admin:ravali" -X PUT http://18.212.25.74:8001/repository/k8s-task/flask:5.0 '
		//flask:3.0.push("latest")
          sh 'docker tag flask:3.0 18.212.25.74:8001/repository/k8s-task/flask:5.0'
          //sh 'docker login -u ravali1505 -p Manoj@123@123'
	  sh 'docker login -u admin -p ravali 18.212.25.74:8001/repository/k8s-task/' 
          sh 'docker push 18.212.25.74:8001/repository/k8s-task/flask:5.0'
          sh 'docker logout http://18.212.25.74:8001/repository/k8s-task/'
            }
          }
       }
    stage('k8s deployment'){
      steps{
        script{
           sh '''
             docker ps
                 sh 'docker push 18.212.25.74:8001/repository/k8s-task/flask:5.0'
                 // docker run -itd --name test-$BUILD_NUMBER 547480451431.dkr.ecr.ap-south-1.amazonaws.com/testrepo:$BUILD_NUMBER
                 ls -lrth
                 docker ps '''
               }
            }
	}
    }
  }
