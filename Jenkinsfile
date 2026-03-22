pipeline {
  agent any
  
  // FIX 1: The 'tools' block MUST be placed BEFORE the 'stages' block.
  tools {
    maven 'maven 3.9.12' // Ensure this exactly matches the case/spelling in Global Tool Configuration
  }
  
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
        
        // FIX 2: Added #!/bin/bash shebang to the top of the multi-line shell script 
        // to ensure it correctly processes variables like $(echo...)
        sh '''#!/bin/bash
GIT_SHORT_COMMIT=$(echo $GIT_COMMIT | cut -c 1-7)
mvn versions:set -DnewVersion="$GIT_SHORT_COMMIT"
mvn versions:commit'''
        
        sh 'mvn package -DskipTests'
        
        // FIX 3: Added the explicit "artifacts:" parameter name which is required in Declarative
        archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
      }
    }
  }
  
  post {
    always {
      echo 'This pipeline is completed..'
    }
  }
}
