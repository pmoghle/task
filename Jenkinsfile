pipeline {
  environment {
    registry = "18.212.25.74:8001/repository/k8s-task/"
    registryCredential = 'nexus'
    dockerImage = ''
    SCANNER_HOME = tool 'SonarQubeScanner'
    }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git branch: 'main', url: 'https://github.com/ganigapetaravali/task.git'
      }
    }
//  stage('Sonarqube') {
//    scannerHome = tool 'SonarQubeScanner'
//     }
//     steps {
//         withSonarQubeEnv('sonarqube') {
//             sh "${scannerHome}/bin/sonar-scanner"
//         }
//         timeout(time: 10, unit: 'MINUTES') {
//             waitForQualityGate abortPipeline: true
//         }
//     }
// }
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
     }
}
// stage('SonarQube analysis') {
//         script {
//           // requires SonarQube Scanner 2.8+
//         //  scannerHome = tool 'SonarQube Scanner 2.8'
//         }
// 	// node('SonarQube Scanner')
//         withSonarQubeEnv('SonarQube Scanner') {
//           sh "${scannerHome}/home/ec2-user/opt/sonar-scanner-4.6.2.2472-linux/bin"
//         }
//       }
  stage('Code Quality Check via SonarQube') {
  // steps {
       script {
//        #!/usr/bin/env groovy
//        import hudson.model.*
//        node('master') {
//        sh("your shell script") 
// 	   }
       def scannerHome = tool 'SonarQube Scanner';
           withSonarQubeEnv("SonarQube Scanner") {
           sh "${tool("sonarqube")}/home/ec2-user/opt/sonar-scanner-4.6.2.2472-linux/bin/sonar-scanner \
          // -Dsonar.projectKey=test-node-js \
           //-Dsonar.sources=. \
           //-Dsonar.css.node=. \
            -Dsonar.host.url=http://34.224.97.242:9000 \
            -Dsonar.login=sqa_2dfbc400bdceb92e733e5c6806316616f9d29581-from-SonarQube Scanner"
               }
      //     }
       }
   }
 withSonarQubeEnv('My SonarQube Server', envOnly: true) {
  // This expands the evironment variables SONAR_CONFIG_NAME, SONAR_HOST_URL, SONAR_AUTH_TOKEN that can be used by any script.
  println ${env.SONAR_HOST_URL} 
}
