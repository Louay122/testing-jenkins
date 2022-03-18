pipeline{
    agent any

    environment{
        DOCKERHUB_CREDENTIALS=credentials('docker_hub')

    }

    stages{
        
        stage('Build'){

            steps{
                sh 'docker build -t louay112/my-app:1.0 .'
            }

        }

        stage('Login'){
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }

        }
        stage('Push'){

            steps{
                sh 'docker push louay112/testing-repo'
            }

        }
    }
    post{
        always{
            sh 'docker logout'
        }
    }
}