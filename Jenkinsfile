pipeline {
  agent any
  
      environment {
          loadEnvFile()
      }
      
    stages {
      stage("EchoNumber") {
          steps {
              sh 'echo $DOCKER_USER'
              echo "RUNNING ON ${BUILD_NUMBER}"
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
def loadEnvFile() {
    def envFile = readFile('.env')
    envFile.readLines().each { line ->
        if (line.trim() && !line.startsWith("#")) {
            def keyValue = line.tokenize('=')
            if (keyValue.size() == 2) {
                env."${keyValue[0].trim()}" = keyValue[1].trim()
            }
        }
    }
}
}

