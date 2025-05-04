pipeline{
    agent any;
    stages{
        stage("Code Clone wala stage"){
            steps{
                git url: "https://github.com/Srichandan1998/two-tier-flask-app.git", branch: "master"
            }
        }
        stage("Build wala stage"){
            steps{
                sh "docker build -t wow-flask-app-wow ."
            }
        }
        stage("Docker Hub Pus wala stage"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "dockerHubCred",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag wow-flask-app-wow  ${env.dockerHubUser}/wow-flask-app-wow "
                sh "docker push ${env.dockerHubUser}/wow-flask-app-wow:latest "
                    
                }
            }
        }
        stage("Deploy wala stage"){
            steps{
                sh "docker compose up -d --build "
            }
        }
    }
}
