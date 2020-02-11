pipeline {
  agent any

  def mvnHome {
    mvnHome = tool 'Maven'
  }  
  stages {
   stage('SCM Checkout') { // for display purposes

      // Get some code from a GitHub repository

      git 'https://github.com/nazir-alam/maven2-check.git'

      // Get the Maven tool.

      // ** NOTE: This 'M3' Maven tool must be configured

      // **       in the global configuration. 
      
   }
   }

      stage('Build') {
 
          // Run the maven build

         withEnv(["MVN_HOME=$mvnHome"]) {

         if (isUnix()) {
 
           sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'

         } else {

            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)

         }

      }

   }
  
   stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
   
   stage('Deploy') {
      deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:8090/')], contextPath: null, war: '**/*.war'
    }
}
