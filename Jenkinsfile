pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("jayajenkins/app")
                }
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3000:3000 jayajenkins/app'
            }
        }
    }
}
