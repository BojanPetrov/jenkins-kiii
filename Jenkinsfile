pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            steps {
                script {
                    def app = docker.build("bojanpetrov/jenkins-kiii")
                }
            }
        }

        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        docker.image("bojanpetrov/jenkins-kiii:${env.BRANCH_NAME}-${env.BUILD_NUMBER}").push()
                        docker.image("bojanpetrov/jenkins-kiii:${env.BRANCH_NAME}-latest").push()
                        // signal the orchestrator that there is a new version
                    }
                }
            }
        }
    }
}
