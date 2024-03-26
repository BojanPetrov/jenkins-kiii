node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("bojanpetrov/jenkins-kiii")
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.main}-${env.BUILD_NUMBER}")
            app.push("${env.main}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}
