pipeline {
   agent any
   environment {
     SONAR_TOKEN = 'b00f19582ca4b27228d2bda2354f883dba10c4b2'
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
    stage('SonarQube Scan') {
       steps{
         withSonarQubeEnv('SonarCloud') {
           sh 'mvn sonar:sonar -Dsonar.projectKey=$SONAR_PROJECT_KEY -Dsonar.login=$SONAR_TOKEN'
         }
      }
    }
    stage('Deploying application ') {
       steps {
           script{
             withEnv(['JENKINS_NODE_COOKIE=dontkill']) {
                   sh 'nohup java -jar ./target/springboot-bootcamp-0.0.1-SNAPSHOT.jar &'
                   }
               }
           }
     }
  }       
} 
    
