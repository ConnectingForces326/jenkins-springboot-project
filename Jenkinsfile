pipeline {
  agent any
  stages {
    stage('Checkout') { steps { checkout scm } }

    stage('Prep') {
      steps {
        sh 'chmod +x mvnw'
      }
    }

    stage('Build') {
      steps { sh './mvnw -B -DskipTests clean package' }
      post { success { archiveArtifacts '**/target/*.jar' } }
    }

    stage('Test') {
      steps { sh './mvnw -B test' }
      post { always { junit '**/target/surefire-reports/*.xml' } }
    }
  }
}
