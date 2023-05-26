pipeline {
    agent any
    triggers {
        pollSCM("H * * * *")
    }
    environment {
        DEPLOY_NUMBER = "${BUILD_NUMBER}"
    }
    stages {
      
        stage("Build") {
            steps {
                sh "dotnet build"
                sh "docker compose build"
            }
        }
        stage("Deliver") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'DH_PASSWORD', usernameVariable: 'DH_USERNAME')]) {
                    sh 'docker login -u $DH_USERNAME -p $DH_PASSWORD'
                    sh "docker compose push"
                }
            }
        }
        stage('Deploying React.js container to Kubernetes') {
            steps {
                script {
                    kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
                }
            }
        }
        
        stage("Deploy") {
            steps {
                build job: 'SynopsisRollback', parameters: [[$class: 'StringParameterValue', name: 'DEPLOY_NUMBER', value: "${BUILD_NUMBER}"]]
            }   
        }
    }
}
