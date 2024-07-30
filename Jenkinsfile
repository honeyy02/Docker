
pipeline {
  agent any
  stages {
     stage('Checkout') {
            steps {
               checkout scm
            }
        }
    stage('Docker Build') {
      steps {
        sh 'docker build -t honeyy02/hello-world-java .'
      }
    }
    stage('Docker Run') {
      steps {
        sh 'docker run honeyy02/hello-world-java'
      }
    }
  }
}
