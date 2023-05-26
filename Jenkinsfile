pipeline {
  agent any
    stages {
      stage("EchoNumber") {
          steps {
              echo "RUNNING ON ${BUILD_NUMBER}"
          }
      }
  
      stage("Build") {
          steps {
              sh "dotnet build --configuration Release"
              sh "docker compose --env-file .env build"
          }
      }
      
      stage("Clean containers") {
                  steps {
                      script {
                          try {
                              sh "docker compose --env-file .env down"
                          }
                          finally { }
                      }
                  }
              }

      stage("Push to registry") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'DH_PASSWORD', usernameVariable: 'DH_USERNAME')]) {
                    sh 'docker login -u $DH_USERNAME -p $DH_PASSWORD'
                    sh "docker compose --env-file .env push"
                }
            }
        }
}
}