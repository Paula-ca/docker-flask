pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    RepoDockerHub = 'pgonzalez' 
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
    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
      sh '''
        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
      '''
    }
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
