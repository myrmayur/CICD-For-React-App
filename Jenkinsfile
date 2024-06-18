pipeline {
    agent any

    tools {
        nodejs 'NodeJs' // This should match the name you gave in the Global Tool Configuration
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
        }pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Ensure this matches the name in Global Tool Configuration
    }

    environment {
        GITHUB_CREDENTIALS = credentials('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') // The ID of the credentials added in Jenkins
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
                sh 'npm install' // Install NodeJS dependencies
            }
        }

        stage('Start Application') {
            steps {
                sh 'npm start' // Ensure the npm start script is correctly configured in package.json
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
