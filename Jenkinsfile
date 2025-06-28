pipeline{
  agent any
  environment{
    IMAGE_NAME = 'mkwak718/test-flask'
  }
  stages{
    stage('Checkout'){
      steps{
        git branch: 'main', url: 'https://github.com/mkwak718/test-flask'
      }
    }
    stage('Build Docker Image'){
      steps{
        sh 'docker build -t %IMAGE_NAME%latest .'        
      }
    }
    stage('Push to Dockerhub'){
      steps{
        withCredentials([usernamePassword(credentialId: 'docker', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
          sh echo %DOCKER_PASS% \
            docker login -u %DOCKER_USER% --password-stdin \
            docker push %IMAGE_NAME%:latest \
            docker logout          
        }
      }
    }
  }
}
