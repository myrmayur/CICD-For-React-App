pipeline {
    agent any
    
    environment {
        GITHUB_REPO_URL = 'https://github.com/myrmayur/my-app.git'
        DOCERHUB_CREDENTALS = 'Dockerhub'
        DOCKER_REPO = 'myrmayur/testapp'
    }
    
    
    stages {
        stage('Checkout') {
            steps {
                git url: "${env.GITHUB_REPO_UR}"
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
                    dockerImage = docker.build("${env.DOCKER_REPO}")
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${env.DOCERHUB_CREDENTALS}") {
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
