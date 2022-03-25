pipeline{
    agent any

    environment{
        DOCKERHUB_CREDENTIALS=credentials('docker_hub')
        registryCredentials = "nexus"
        registry = "http://localhost:8081/repository/docker-private-repo/"
    }

    stages{
        
        stage('Build'){

            steps{
                sh 'docker build -t louay112/my-app:1.0 .'
            }

        }

        stage('Uploading to Nexus') {
            steps{  
                script {
                    docker.withRegistry( registry, registryCredentials ) {
                    dockerImage.push('louay112/my-app:1.0')
                     }
                 }
             }
        }
        
    }
    post{
        always{
            sh 'docker logout'
        }
    }
}