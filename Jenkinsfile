pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Test') {
            steps {
                bat 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t devops-exp10 .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat 'docker rm -f devops-exp10-container || exit /b 0'
                bat 'docker run -d --name devops-exp10-container -p 3000:3000 devops-exp10'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'curl http://localhost:3000/health'
            }
        }
    }

    post {
        success {
            echo 'DevOps pipeline completed successfully.'
        }

        failure {
            echo 'DevOps pipeline failed.'
        }
    }
}