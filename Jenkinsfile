pipeline{
    agent any
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/Ashwini2593/node-todo-cicd.git", branch: 'master'
                echo "Code clone ho gaya hai"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build . -t node-app-demo"
                echo "docker build bhi ho chuka hai"
            }
        }   
        stage("Push to Repository"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker tag node-app-demo ${env.dockerHubUser}/node-app-demo-ashwini:latest"
                    sh "docker push ${env.dockerHubUser}/node-app-demo-ashwini:latest"
                }
                echo "DockerHub pe push ho gaya hai" 
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose up -d"
                echo "AWS EC2 pe docker compose ne deploy kar diya hai"
            }
        }
                
    }
}
