pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Compiling sysfoo app..'
        sh 'mvn compile'
      }
    }

    stage('Test') {
      steps {
        echo 'Running Unit Testing..'
        sh 'mvn clean test'
      }
    }

    stage('Package') {
      steps {
        echo 'Creating package for the app....'
        sh 'mvn package -DskipTests'
      }
    }

  }
  tools {
    maven 'maven 3.9.12'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}