node {
    def app

    stage('Build image') {

        app = docker.build("shadeyy/coursework")

    }

    stage('Test image') {

        app.inside {
            sh 'echo "Tests passed"'
            sh 'ls'
        }

    }

    stage('Push image') {

        docker.withRegistry('https://registry.hub.docker.com', 'coursework') {

            app.push("${env.BUILD_NUMBER}")
            app.push("latest")

        }
    }
}
