pipeline {

    agent any
    environment {
        DOCKER_IMAGE_NAME = 'vikasdfghjl/landing_page'
    }

    tools{
        dockerTool 'Docker'
        nodejs 'Node-18.16.1'
     }

    stages{
        stage("build"){
            steps{
                echo "Executing npm"
                sh 'npm install'
            }
        }

        stage("Docker build and Push"){
            steps{
                script{

                    withCredentials([usernamePassword(credentialsId: 'DOCKERHUB_CREDS', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                        sh 'echo "$DOCKERHUB_PASSWORD" | docker login -u "$DOCKERHUB_USERNAME" --password-stdin '

                        def app = docker.build("vikasdfghjl/landing_page")

                        app.push("latest")
                        }
                }
            }
        }        

    }

}