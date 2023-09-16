pipeline {
  agent any
  environment{
    DOCKERHUB_CREDENCIALS = credentials ('dockerhub')
    RepoDockerHub = 'lferraro11'
    NameContainer = 'docker-flask'
  }
  stages {
    stage('Build'){
      steps{
        sh "docker build -t ${env.RepoDockerHub}/${env.NameContainer}:${env.BUILD_NUMBER} ."
      }
    }
    stage('Login to Dockerhub'){
      steps{
        sh "echo $DOCKERHUB_CREDENCIALS_PSW | docker login -u $DOCKERHUB_CREDENCIALS_USR --password-stdin"
      }
    }
    stage('Push image to Dockerhub'){
      steps{
        sh "docker push ${env.RepoDockerHub}/${env.NameContainer}:${env.BUILD_NUMBER} "
      }
    }
  }
}
