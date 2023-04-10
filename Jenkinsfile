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
}
             
  
    
