node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("BojanPetrov/jenkins-kiii")
    }
    stage('Push image') {   
    withEnv(["DOCKER_PASSWORD=Neosonic-11"]) {
        sh 'echo $DOCKER_PASSWORD | docker login -u bojanpetrov --password-stdin'
        docker.withRegistry('https://index.docker.io/v1/', 'bojanpetrov', 'Neosonic-11') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}
}
