pipeline {
  agent any

  options {
    disableConcurrentBuilds()
    buildDiscarder(logRotator(numToKeepStr: '5')
  }

  stages{
    stage('Checkout') {
        steps {
            checkout scm
        }
    }

    stage('Build') {
        steps {
            sh './gradlew.assemble'
        }
    }

    stage('Test') {
        steps {
            sh './gradlew test'
        }

        post {
            always {
                junit '**/build/test-result/test/*.xml'
            }
        }
    }
  }

  post {
    success {
        echo 'Build succeeded!'
    }
    failure {
        echo 'Build failed!'
    }
  }


}
