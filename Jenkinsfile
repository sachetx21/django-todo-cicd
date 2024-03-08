pipeline {
    agent any
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/sachetx21/django-todo-cicd.git", branch: "develop"
                echo 'bhaiyya code clone ho gaya'
            }
        }
        stage("build"){
            steps{
                sh "docker build -t django-todo-cicd-web ."
                echo 'code build bhi ho gaya'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHubCreds",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag django-todo-cicd-web:latest ${env.dockerHubUser}/django-todo-cicd-web:latest"
                sh "docker push ${env.dockerHubUser}/django-todo-cicd-web:latest"
                echo 'image push ho gaya'
                }
            }
        }
        stage("deploy"){
            steps{
                #sh "docker-compose down && docker-compose up -d"
                echo 'deployment ho gayi'
            }
        }
    }
}
