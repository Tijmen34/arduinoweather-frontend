node('swarm-build-agent') {
    def app

    stage('Checkout SCM') {
        checkout scm
    }

    stage('Build') {
        app = docker.build("tijmen34/arduinoweather-frontend")
    }
    stage('Push Image') {
        docker.withRegistry('https://registry.hub.docker.com', 'tijmen34-dockerhub-creds') {
            app.push("${env.BUILD_NUMBER}")
            app.push("lts")
        }
    }
    stage('Deploy') {
         sh "docker service update --image tijmen34/arduinoweather-frontend:${env.BUILD_NUMBER} arduino-frontend"
    }
}
