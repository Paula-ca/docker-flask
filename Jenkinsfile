pipeline {
  agent any
  stages {
    stage('Build'){
      steps{
        sh "docker build -t lferraro11/docker-flask:${env.BUILD_NUMBER} ."
      }
    }
  }
}
