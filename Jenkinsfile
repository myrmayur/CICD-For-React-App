pipeline {
    agent any

    tools {
        nodejs 'NodeJS 14' // This should match the name you gave in the Global Tool Configuration
    }

    environment {
        GITHUB_CREDENTIALS = credentials('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') // Use the ID of the credentials you added
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository using the credentials
                git url: 'https://github.com/myrmayur/my-app.git', branch: 'master', credentialsId: "${GITHUB_CREDENTIALS}"
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm start'
            }
        }

        
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
