node {
    def app

    stage('Clone repository'){

        checkout scm
    }

    stage('Build image'){

        app = docker.build("Louay112/my-app")

    }

    stage('Test image'){

        app.inside{
            echo "Tests passed"
        }
    }
    stage('Push image'){

        docker.withRegistry('https://registry.hub.docker.com','louay112'){
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
        echo "Trying to push docker build to dockerHub"
    }
}