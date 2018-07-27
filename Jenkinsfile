pipeline {
  agent any
  stages {
    stage('checkout project') {
      steps {
        checkout scm
      }
    }
    stage('test') {
      steps {
        sh 'mvn clean cobertura:cobertura test'
      }
    }
    stage('report') {
      parallel {
        stage('report') {
          steps {
            junit 'target/surefire-reports/*.xml'
          }
        }
        stage('error') {
          steps {
            cobertura(classCoverageTargets: 'target/site/cobertura/coverage.xml')
          }
        }
      }
    }
    stage('package') {
      steps {
        sh 'mvn package '
      }
    }
    stage('archive') {
      steps {
        archiveArtifacts 'deploy/release/spring-boot-sample-data-rest-0.1.0.jar'
      }
    }
    stage('deploy') {
      steps {
        sh 'make deploy-default'
      }
    }
  }
  post {
    always {
      echo 'I will always say Hello again!'

    }

    success {
      echo 'success!'

    }

    failure {
      echo 'failure!'

    }

  }
}