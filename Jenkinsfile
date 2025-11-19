pipeline{
  agent any
  environment{
    IMAGE_NAME = "irfanvox/test-flask-jenkins"
  }
  stages{
    stage("Checkout git"){
      steps{
        git branch: 'main', url: "https://github.com/irfanvox/test-flask-jenkins"
      }
    }
    stage("Build Docker image"){
      steps{
        sh "docker build -t $IMAGE_NAME:latest ."
      }
    }
    stage("Push to DockerHub"){
      steps{
        withCredentials([usernamePassword(credentialsId: "docker", usernameVariable: "DOCKER_USER", passwordVariable: "DOCKER_PASS")]){
          sh """
          echo $DOCKER_PASS |
          docker login -u $DOCKER_USER --password-stdin
          docker push $IMAGE_NAME:latest
          docker logout
          """
        }
      }
    }
  }
}
