pipeline {

  // environment {
  //   dockerimagenameapi = "faustis1337/search-engine-api-search"
  //   dockerimagenameweb = "faustis1337/search-engine-frontend"
  //   dockerimagenameload = "faustis1337/search-engine-searchloadbalancer"
  //   dockerImageApi = ""
  //   dockerImageWeb = ""
  //   dockerImageLoad = ""
  // }

  agent any

  stages {
  
  // stage('Checkout Source') {
  //       steps {
  //         git 'https://github.com/Natorden/JenkinsTest'
  //       }
  //     }
  
    stage('Build image') {
      steps{
      echo 'build image'
//       sh 'docker-compose build'  
//         script {
//           dockerImageApi = docker.build dockerimagenameapi
//           dockerImageWeb = docker.build dockerimagenameweb
//           dockerImageLoad = docker.build dockerimagenameload
//         }
        
      }
    }
    
//         stage('Deploy') {
//           steps{
//                 sh "docker-compose rm"
//                 sh "docker-compose up -d"
//           }
//         }

//     stage('Pushing Image') {
//       environment {
//                registryCredential = 'DockerHub'
//            }
//       steps{
//         script {
//           docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
//             dockerImage.push("latest")
//           }
//         }
//       }
//     }
// 
//     stage('Deploying React.js container to Kubernetes') {
//       steps {
//         script {
//           kubernetesDeploy(configs: "ApiSearch/deploy.yaml", "ApiSearch/service.yaml", "LoadBalancer/deploy.yaml", "LoadBalancer/service.yaml", "WebSearch/deploy.yaml", "WebSearch/service.yaml")
//         }
//       }
//     }
//   }
}
}