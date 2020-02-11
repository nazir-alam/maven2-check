pipeline {
  agent any
  stages {
      stage('SCM Checkout') {
        steps {
checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '104ad4c1-b458-42de-a712-f264f17bb13e', url: 'https://github.com/nazir-alam/maven2-check.git']]])
      
        }
      }

      stage('Build') {
        steps {
          // Run the maven build

         withEnv(["MVN_HOME=$mvnHome"]) {

       //  if (isUnix()) {
 
        //   sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'

       //  } else {

            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)

   //      }

   //   }

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
     steps {
      deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:8090/')], contextPath: null, war: '**/*.war'
    }
  }
  }}
