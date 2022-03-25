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
                sh 'docker build -t my-app .'
            }

        }

        stage('Login'){
            steps{
                sh 'echo $NEXUS_CREDENTIALS_PSW | docker login -u $NEXUS_CREDENTIALS_USR --password-stdin http://localhost:8095/repository/docker-private-repo/'
            }

        }
        stage('Push'){

            steps{
                sh 'docker tag my-app:latest http://localhost:8095/my-app:latest'
                sh 'docker push http://localhost:8095/repository/docker-private-repo/my-app'
            }

        }
    }
    post{
        always{
            sh 'docker logout'
        }
    }
}