pipeline {
  agent any
  
  
    stages {
      stage("EchoNumber") {
          steps {
              echo "RUNNING ON ${BUILD_NUMBER}"
          }
      }
      
      environment {
              DISABLE_AUTH = 'true'
              DB_ENGINE    = 'sqlite'
              DOCKER_USER = credentials('docker-user')
          }
          
      stage("Clean containers") {
                        steps {
                            script {
                                try {
                                sh"echo $$DOCKER_USER"
                                    sh "docker compose --env-file .env down"
                                }
                                finally { }
                            }
                        }
                    }
  
      stage("Build NET") {
          steps {
              sh "dotnet build --configuration Release"

          }
      }
      
      stage("BUILD CONTAINERS") {
                steps {
                    sh "docker compose --env-file .env build"
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