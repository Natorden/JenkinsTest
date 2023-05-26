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
  
      stage("Build") {
          steps {
              sh "dotnet build --configuration Release"
              sh "docker compose build"
          }
      }
      
      stage("Clean containers") {
                  steps {
                      script {
                          try {
                              sh "docker-compose down"
                          }
                          finally { }
                      }
                  }
              }

      stage("Push to registry") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'DH_PASSWORD', usernameVariable: 'DH_USERNAME')]) {
                    sh 'docker login -u $DH_USERNAME -p $DH_PASSWORD'
                    sh "docker compose push"
                }
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