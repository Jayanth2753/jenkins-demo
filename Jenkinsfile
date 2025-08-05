pipeline {
  agent {
    docker {
      image 'docker:latest'
      args '-v /var/run/docker.sock:/var/run/docker.sock'
    }
  }

  stages {
    stage('Build Docker Image') {
      steps {
        echo 'Building Docker image...'
        sh 'docker build -t jayajenkins/app .'
      }
    }
    stage('Run Container') {
      steps {
        echo 'Running container...'
        sh 'docker run -d -p 3000:3000 jayajenkins/app'
      }
    }
  }
}
