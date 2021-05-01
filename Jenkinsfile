pipeline{   
    agent any
  stages{
         stage('scm checkout'){
             steps{
              git credentialsId: 'github', url: 'https://github.com/govinda143/skillenzahcl.git'
             }
         }
         stage('sonar qube'){
             steps{
                 script{
                 withSonarQubeEnv(credentialsId: 'sonarserver') {
                     sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
                    }
                 }
             }
         }
           stage("Quality Gate"){
           steps{
               script{
                   timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
           def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
          if (qg.status != 'OK') {
          error "Pipeline aborted due to quality gate failure: ${qg.status}"
               }
           }
         }
      }
    }
         
         stage ('mvn build'){
               steps{
                 sh "mvn clean package"
                 
             }
         }
     }
}
