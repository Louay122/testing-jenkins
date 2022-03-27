pipeline{
    agent any

    environment{
        DOCKERHUB_CREDENTIALS=credentials('docker_hub')
        NEXUS_CREDENTIALS = credentials('nexus')
        registry = "http://localhost:8095/repository/docker-private-repo/"
    }

    stages{
        
        stage('Build'){

            steps{
                //sh 'docker build -t my-app .'
                script {
                    dockerImage = docker.build my-app
                }
            }

        }

        stage('Login'){
            steps{
                sh 'echo $NEXUS_CREDENTIALS_PSW | docker login -u $NEXUS_CREDENTIALS_USR --password-stdin http://localhost::8095/repository/docker-private-repo/'
            }

        }
        stage('Push'){

            steps{
                //sh 'docker tag my-app:latest https://a200-197-15-103-222.ngrok.io:8095/docker-private-repo/my-app:latest'
                //sh 'docker push https://a200-197-15-103-222.ngrok.io:8095/docker-private-repo/my-app:latest'
                script {
                    docker.withRegistry( registry, NEXUS_CREDENTIALS ) {
                    dockerImage.push('latest')
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