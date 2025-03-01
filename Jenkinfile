pipeline {
    
    agent any
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/Srichandan1998/two-tier-flask-app.git" , branch: "master"
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t flaskpraticeimage  ."
            }
        }
        stage("Test"){
            steps{
                echo "Test wali code"
            }    
        }
        stage("Docker Hub Push"){
            steps{
                withCredentials([usernamePassword(
                  credentialsId: "dockerHubCreds",
                  passwordVariable: "dockerHubPass",
                  usernameVariable: "dockerHubUser"
                )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag flaskpraticeimage  ${env.dockerHubUser}/flaskpraticeimage "
                sh "docker push ${env.dockerHubUser}/flaskpraticeimage:latest "
                
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build "
            }
        }
    }
}
