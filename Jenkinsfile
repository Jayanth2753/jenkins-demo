pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Running basic checks...'
                bat 'dir'
                bat 'type index.html'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying using Docker...'
                bat 'docker build -t jenkins-ci-demo .'
                bat '''
                docker stop jenkins-app || echo "Container not running"
                docker rm jenkins-app || echo "Container not found"
                docker run -d -p 8081:80 --name jenkins-app jenkins-ci-demo
                '''
            }
        }
    }
}