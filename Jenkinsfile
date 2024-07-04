pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = 'Dockerhub'
        DOCKER_HUB_REPO = 'myrmayur/testapp'
        GIT_REPO_URL = 'https://github.com/myrmayur/my-app.git'
        GIT_CREDENTIALS_ID = 'Github'
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: "${env.GIT_CREDENTIALS_ID}", url: "${env.GIT_REPO_URL}"
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build("${env.DOCKER_HUB_REPO}")
                }
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${env.DOCKER_HUB_CREDENTIALS}") {
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
