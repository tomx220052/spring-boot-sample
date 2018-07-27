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
    stage('package') {
      parallel {
        stage('package') {
          steps {
            sh 'mvn package '
          }
        }
        stage('report') {
          steps {
            junit 'target/surefire-reports/*.xml'
          }
        }
        stage('') {
          steps {
            cobertura(classCoverageTargets: 'target/site/cobertura/coverage.xml')
          }
        }
      }
    }
    stage('archive') {
      steps {
        archiveArtifacts 'target/spring-boot-sample-data-rest-0.1.0.jar'
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