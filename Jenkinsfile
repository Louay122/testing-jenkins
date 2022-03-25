pipeline{
    agent any

    environment{
        DOCKERHUB_CREDENTIALS=credentials('docker_hub')
        NEXUS_CREDENTIALS = credentials('nexus')
        registry = "http://localhost:8081/repository/docker-private-repo/"
    }

    stages{
        
        stage('Build'){

            steps{
                sh 'docker build -t my-app:1.0 .'
            }

        }

        stage('Login'){
            steps{
                sh 'docker login -u admin -p Sprayos112345+ http://localhost:8095'
            }

        }
        stage('Push'){

            steps{

                sh 'docker push http://localhost:8081/repository/docker-private-repo/my-app:1.0'
            }

        }
    }
    post{
        always{
            sh 'docker logout'
        }
    }
}