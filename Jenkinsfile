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
                    timeout(time: 5, unit: 'MINUTES) {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                     error "Pipeline aborted due to quality gate failure: ${qg.status}"
                 }
             }
             sh "mvn clean package"
         }
        }
      }
  }
}
