
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
    stage('Docker Login') {
      steps {
        withCredentials([string(credentialsId: 'docker_hub_credentials', variable: 'DOCKERHUB_PASSWORD')]) {
          sh 'echo $DOCKERHUB_PASSWORD | docker login -u honeyy02 --password-stdin'
      }
    }
    }
    stage('Docker Push') {
      steps {
        sh 'docker push honeyy02/hello-world-java'
      }
    }
  }
}
