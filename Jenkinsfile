pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'chaitanyatholada/movers-and-packers:latest'  
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/TholadaChaitanya/Packers-and-Movers.git'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t ${DOCKER_IMAGE} .'
            }
        }

        stage('Docker Push') {
            steps {
                withDockerRegistry(credentialsId: 'docker-credentials', url: 'https://index.docker.io/v1/') {
                    sh 'docker push ${DOCKER_IMAGE}'
                }
            }
        }
    }
}
