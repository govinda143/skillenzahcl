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
             
         stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
         
         stage ('mvn build'){
               steps{
                 sh "mvn clean package"
                 
             }
         }
     }
}
