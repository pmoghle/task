pipeline {
  environment {
    registry = "18.212.25.74:8001/repository/k8s-task/"
    registryCredential = 'nexus'
    dockerImage = ''
    SCANNER_HOME = tool '/home/ec2-user/opt/sonar-scanner-4.6.2.2472-linux'
    }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git branch: 'main', url: 'https://github.com/ganigapetaravali/task.git'
      }
    }
  stage('SonarQube analysis') {
    steps {
    withSonarQubeEnv(credentialsId: 'sqa_2dfbc400bdceb92e733e5c6806316616f9d29581', installationName: 'Sonar') {
         sh '''$SCANNER_HOME/bin/sonar-scanner \
         -Dsonar.projectKey=k8s-task2 \
         -Dsonar.projectName=k8s-task \
         -Dsonar.sources=src/ \
         -Dsonar.java.binaries=target/classes/ \
         -Dsonar.exclusions=src/test/java/****/*.java \
         -Dsonar.java.libraries=/var/lib/jenkins/.m2/**/*.jar \
         -Dsonar.projectVersion=${BUILD_NUMBER}-${GIT_COMMIT_SHORT}'''
       }
     }
   }
  stage('SQuality Gate') {
     steps {
       timeout(time: 1, unit: 'MINUTES') {
       waitForQualityGate abortPipeline: true
       }
     }
   }
   stage('Building image') {
      steps{
        script {
          sh 'docker build -t flask:6.0 .'
        }
       }
	  }
    stage('Deploy Image in to nexus registry') {
      steps{
        script {
	   //sh 'curl "admin:ravali" -X PUT http://18.212.25.74:8001/repository/k8s-task/flask:5.0 '
		//flask:3.0.push("latest")
          sh 'docker tag flask:3.0 18.212.25.74:8001/repository/k8s-task/flask:6.0'
          //sh 'docker login -u ravali1505 -p Manoj@123@123'
	  sh 'docker login -u admin -p ravali 18.212.25.74:8001/repository/k8s-task/' 
          sh 'docker push 18.212.25.74:8001/repository/k8s-task/flask:6.0'
          sh 'docker logout http://18.212.25.74:8001/repository/k8s-task/'
            }
          }
       }
     
