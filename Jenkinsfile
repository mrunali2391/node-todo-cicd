pipeline{
    agent { label 'dev-agent' }
    stages{
        stage("code"){
            steps{
                git url: "https://github.com/mrunali2391/node-todo-cicd.git", branch: "master"
            }
            
        }
        
        stage("build and push to dockerhub"){
            steps{
                sh 'docker build . -t mrunali23/node-todo-app:latest'
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPassword",usernameVariable:"dockerhubUsername")]){
                    sh "docker login -u ${env.dockerhubUsername} -p ${env.dockerhubPassword}"
                    sh "docker push mrunali23/node-todo-app:latest"
                }
            }
        }
        
        stage("deploy"){
            steps{
        sh 'docker-compose down && docker-compose up -d'   
            }
        }
    }
}
