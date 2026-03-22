pipeline {
  agent any

  tools {
    maven 'maven 3.9.12'
  }
  
  stages {
    stage('Build') {
      steps {
        echo 'Compiling sysfoo app..'
        bat 'mvn compile'
      }
    }

    stage('Test') {
      steps {
        echo 'Running Unit Testing..'
        bat 'mvn clean test'
      }
    }

    stage('Package') {
      steps {
        echo 'Creating package for the app....'
        bat 'mvn package -DskipTests'
      }
    }

  }
  
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}
