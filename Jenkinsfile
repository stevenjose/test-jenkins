pipeline {
  agent any
  tools {
    nodejs 'node-20.5.1'
    docker
  }

  options {
    timeout(time: 2, unit: 'MINUTES')
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
        sh "docker pull docker.artifactory.company.com/util-sonar-runner:latest"
          withSonarQubeEnv('sonarqube'){
          sh "docker run --rm -v ${workspace}:/opt/spring-service -w /opt/spring-service -e SONAR_HOST_URL=${SONAR_HOST_URL} -e SONAR_AUTH_TOKEN=${SONAR_AUTH_TOKEN} docker.artifactory.company.com/util-sonar-runner:latest /opt/sonar-scanner/bin/sonar-scanner -Dsonar.host.url=${SONAR_HOST_URL} -Dsonar.login=${SONAR_AUTH_TOKEN} -Dsonar.projectKey=spring-service -Dsonar.projectName=spring-service  -Dsonar.projectBaseDir=. -Dsonar.sources=./src -Dsonar.java.binaries=./build/classes -Dsonar.junit.reportPaths=./build/test-results/test -Dsonar.jacoco.reportPaths=./build/jacoco/test.exec -Dsonar.exclusions=src/test/java/**/* -Dsonar.fortify.reportPath=fortifyResults-${IMAGE_NAME}.fpr -Dsonar.password="
        } 
      }     
    }
  }
}
