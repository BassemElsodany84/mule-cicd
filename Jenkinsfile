pipeline {
  agent any
  tools {
    maven 'apache-maven-3.6.1'
  }
  stages {
    stage('Unit Test') { 
      steps {
        sh 'mvn clean test'
      }
    }
    stage('Deploy Standalone') { 
      steps {
        sh 'mvn deploy -P standalone'
      }
    }
    stage('Deploy ARM') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials') 
      }
      steps {
        sh 'mvn deploy -P arm -Darm.target.name=local-3.9.0-ee -Danypoint.username=${ANYPOINT_CREDENTIALS_USR}  -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW}' 
      }
    }
    stage('Deploy CloudHub') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypoint.credentials')
      }
      steps {
        sh 'mvn deploy -P cloudhub -DmuleDeploy' 
      }
    }
  }
}