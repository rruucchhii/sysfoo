pipeline {
  agent any
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
        sh '''#truncate the git_commit to the 7 character
GIT_SHORT_COMMIT=$(echo $GIT_COMMIT | cut -c 1-7)
#set the version using maven
mvn versions:set -DnewVersion="$GIT_SHORT_COMMIT"
mvn versions:commit'''
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