pipeline {
   agent any
   environment {
     SONAR_TOKEN = 'd523c3c155bd8070236b7dd4ec53cc024d62a3d7'
     SONAR_PROJECT_KEY = 'Shekhar9897_sonarqube'
       }
   stages {
   stage('Installing Maven') {
      steps {
          sh 'sudo apt-get update -y && sudo apt-get upgrade -y'
          sh 'sudo apt-get install -y wget tree unzip maven'
           }
        }
    stage('Compiling and running test cases') {
       steps {
           sh 'mvn clean'
           sh 'mvn compile'
           sh 'mvn test'
       }
    }
    stage('creating Package') {
       steps {
           sh 'mvn package'
         }
      }
    stage('Build') {
       steps {
           sh 'mvn clean package'
         }
      }
    stage('SonaQube Scan') {
       steps {
           withSonarQubeEnv('SonarCloud') {
             sh 'mvn sonar:sonar' -Dsonar.projectKey=$SONAR_PROJECT_KEY -Dsonar.login=$SONAR_TOKEN'
       }
     }
   }
    stage('Check SonarQube Connection') {
  steps {
    script {
      def sonarQubeServer = getSonarQubeServer('SonarCloud')
      if (sonarQubeServer == null) {
        error("SonarQube server not configured in Jenkins")
      } else {
        echo "SonarQube server URL: ${sonarQubeServer.url}"
        echo "SonarQube server authentication token: ${sonarQubeServer.credentialsId}"
           }
         }  
       }
     }
  }       
} 
    
