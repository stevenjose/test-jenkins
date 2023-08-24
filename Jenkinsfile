pipeline {
  agent any
  tools {
    nodejs 'node-20.5.1'
  }

  options {
    timeout(time: 5, unit: 'MINUTES')
  }

  stages {
    stage('Install dependencies') {
      steps {
        sh 'npm i'
      }
    }
    stage('Run tests') {
      steps {
        sh 'npm t'
      }
    }
    stage('Sonar Analysis'){
      steps {
          withSonarQubeEnv('sonarqube'){
          sh "npm sonar"
        } 
      }     
    }
  }
}
