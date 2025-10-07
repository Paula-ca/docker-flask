pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    RepoDockerHub = 'paula-ca'  // <-- cambiá esto a tu usuario real de DockerHub
    NameContainer = 'flask-hello-world'
  }
  stages {
    stage('Build') {
      steps {
        sh "docker build -t ${env.RepoDockerHub}/${env.NameContainer}:${env.BUILD_NUMBER} ."
      }
    }
    stage('Login to Dockerhub') {
      steps {
        sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
      }
    }
    stage('Push image to Dockerhub') {
      steps {
        sh "docker push ${env.RepoDockerHub}/${env.NameContainer}:${env.BUILD_NUMBER}"
      }
    }
    stage('Deploy container') {
      steps {
        sh """
          docker stop ${env.NameContainer} || true
          docker rm -f ${env.NameContainer} || true
          docker run -d --name ${env.NameContainer} -p 5000:5000 ${env.RepoDockerHub}/${env.NameContainer}:${env.BUILD_NUMBER}
        """
      }
    }
    stage('Docker logout') {
      steps {
        sh "docker logout"
      }
    }
  }
}
