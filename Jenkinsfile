pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t my-flask-app .'
        sh 'docker tag my-flask-app docker_bflask_image'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run my-flask-app python -m pytest app/tests/'
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USER -p $DOCKER_PASSWORD'
        sh 'docker push bmudasir/docker_bflask_image'
        }
      }
    }
  post {
    always {
      sh 'docker logout'
    }
  }
}

