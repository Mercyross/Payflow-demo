pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out PayFlow demo code from GitHub...'
            }
        }

        stage('Build') {
            steps {
                echo 'Simulating build of PayFlow landing page...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running placeholder tests...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying PayFlow landing page to staging...'
                sh 'cp index.html /var/payflow-deploy/index.html'
                echo 'Deployment complete. View it at http://localhost:8081'
            }
        }
    }
}