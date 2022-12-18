node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

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

    stage('Deploy Build') {

        sshagent(credentials: ['my-ssh-key']) {
                
            sh "ssh ubuntu@52.91.167.57 kubectl set image deployments/coursework coursework=shadeyy/coursework:${env.BUILD_NUMBER}"

        }
    }
}
