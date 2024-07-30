pipeline{
    agent any
    environment{
        DOCKER_CREDENTIAL_ID = "docker_hub_credentials"
        DOCKER_IMAGE_NAME = "honeyy02/java-helloworld"
    }
    stages{   
        stage('checkout'){
            steps{
                checkout scm
            }
        }
        stage('Compile') {
            steps{
                
            echo "Building..."
            // Compile the Java code
            sh 'javac Main.java'
            }
        }

        stage('Run') {
            echo "Running..."
            // Execute the Java program
            sh 'java Main'
          } 
        stage ("Build docker image"){
            steps{
                script{
                    docker.build("${DOCKER_IMAGE_NAME}:latest")
                }
            }
        }
        stage('Push the docker image') {
            steps{
                script{
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                    docker.image("${DOCKER_IMAGE_NAME}:latest").push('latest')
                }
            }
        }
    }
      post {
        always {
            // Clean up Docker images to save space
            sh 'docker system prune -af'
        }
    }
}
}    
