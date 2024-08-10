pipeline{
    agent any
    stages{
        stage("Code"){
            steps{
                echo "Bhaiya Github se me Code Clone kr rha hun"
                git url: "https://github.com/manish-g0u74m/node-todo-cicd", branch: "master"
                echo "Bhaiya mera Code Clone ho gye hen"
            }
        }
        stage("Build image and test image"){
            steps{
                echo "Now I am Building an Image"
                sh "docker build -t node-app:latest ."
                echo "Image Build ho gya hen"
            }
        }
        stage("Scaning Image"){
           steps{
                echo "Bhaiya mene Image ko Scane kr liya hen"
            } 
        }
        stage("Push to dockerhub"){
           steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"  
                sh "docker tag node-app:latest ${env.dockerHubUser}/node-app:latest"
                sh "docker push ${env.dockerHubUser}/node-app:latest"
                echo "Build image Dockerhub pr push ho gyi he"
                }
            } 
        }
        stage("Deploy"){
           steps{
                sh "docker-compose down && docker-compose up -d"
                echo "Bhaiya Application Deploy ho Gyi hen"
            } 
        }
    }  
}
