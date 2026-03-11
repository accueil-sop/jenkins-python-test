pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/accueil-sop/jenkins-python-test.git'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 -m unittest discover'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-python-test:latest .'
            }
        }

        stage('Deploy Test Container') {
            steps {
                sh 'docker rm -f jenkins-python-test-container || true'
                sh 'docker run --name jenkins-python-test-container jenkins-python-test:latest'
            }
        }

    }
}