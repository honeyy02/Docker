pipeline {
environment {
   registry = "honeyy02/java-helloworld"
registryCredential = 'docker_hub_credentials'
dockerImage = ''
}
agent any
stages {
stage('Checkout') {
steps {
checkout scm
}
}
stage('Building our image') {
steps{
script {
   sh 'docker login -u honeyy02'
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
}
}
stage('Cleaning up') {
steps{
sh "docker rmi $registry:$BUILD_NUMBER"
}
}
}
}
