pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'chaitanyatholada/movers-and-packers:latest'
        SCANNER_HOME = tool 'Sonar-Scanner'  
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

        stage('Sonarqube Analysis'){
            steps{
                withSonarQubeEnv('Sonar-Server') {
                    sh '$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=MoversAndPackers -Dsonar.projectKey=MoversAndPackers'
                }
            }
        }

        stage('Trivy File Scan') {
            steps {
                retry(3) {
                    sh 'trivy fs --format table -o Files_Scan_report.html .'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t ${DOCKER_IMAGE} .'
            }
        }

        stage('Trivy Image Scan') {
            steps {
                sh 'trivy image --format table -o Image_Scan_report.html ${DOCKER_IMAGE}'
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
