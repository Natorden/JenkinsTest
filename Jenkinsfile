pipeline {

  environment {
    dockerimagenameapi = "nitrozeus1/search-engine-api-search"
    dockerimagenameweb = "nitrozeus1/search-engine-frontend"
    dockerimagenameload = "nitrozeus1/search-engine-searchloadbalancer"
    dockerImageApi = ""
    dockerImageWeb = ""
    dockerImageLoad = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/Natorden/JenkinsTest.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImageApi = docker.build dockerimagenameapi
          dockerImageWeb = docker.build dockerimagenameweb
          dockerImageLoad = docker.build dockerimagenameload
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'DockerHub'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "ApiSearch/deploy.yaml", "ApiSearch/service.yaml", "LoadBalancer/deploy.yaml", "LoadBalancer/service.yaml", "WebSearch/deploy.yaml", "WebSearch/service.yaml")
        }
      }
    }
  }
}