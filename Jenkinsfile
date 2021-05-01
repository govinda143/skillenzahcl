pipeline{   
    agent any

 
     stages{
         stage('scm checkout'){
             steps{
                 https://github.com/govinda143/skillenzahcl.git
             }
         }
         stage('sonar qube'){
             agent{
                 label 'maven'
            }
             steps{
                 script{
                 withSonarQubeEnv(credentialsId: 'sonar2') {
                     sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
                    }
                 }
             }
         }
         
         stage ('mvn build'){
             agent{
                 label 'maven'
         }
             steps{
                 sh "mvn clean package"
                 
             }
         }
