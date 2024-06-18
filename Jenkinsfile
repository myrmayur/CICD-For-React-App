pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your GitHub repository
                git url: 'https://github.com/myrmayur/my-app.git', branch: 'master'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node.js and npm if not already installed (example)
                // nodejs('NodeJS 14') {
                //     sh 'npm install'
                // }
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests using npm
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                // Build the React app for production
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Example: Copy build artifacts to a server or hosting platform
                // Adjust this step based on your deployment target
                sh 'cp -r build/* /path/to/deploy/directory'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
            currentBuild.result = 'SUCCESS'
        }
        failure {
            echo 'Pipeline failed!'
            currentBuild.result = 'FAILURE'
        }
    }
}
