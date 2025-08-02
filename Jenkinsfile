pipeline{
    agent { label "dev"};
    stages{
        stage("Code"){
            steps{
                git url:"https://github.com/Rwadsariya/two-tier-flask-app.git", branch:"main"
                echo "code Clone ho gaya..."
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("Test"){
            steps{
                echo "Developer / Tester likh bhi gaya.."
            }
        }
        stage("push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHubCreds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
                    echo "pushed to Docker Hub"
                    echo "docker login -u ${env.DOCKER_USER} -p {env.DOCKER_PASS}"
                    sh "docker tag two-tier-flask-app ${env.DOCKER_USER}/two-tier-flask-app"
                    sh "docker push ${env.DOCKER_USER}/two-tier-flask-app"
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
                echo "Docker compose se deploy bhi ho gaya"
            }
        }
    }
}
