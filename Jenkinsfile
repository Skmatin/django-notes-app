pipeline {
    agent any
    
    stages {
        stage("Code") {
            steps {
                echo "Cloning the code"
                git url:"https://github.com/Skmatin/django-notes-app.git",branch: "main"
            }
        }
        
        stage("Build") {
            steps {
                echo "Building the code"
                sh "docker build -t notes-app1 ."
            }
        }
        
        stage("Push the code") {
            steps {
                echo "Pushing the code to dockerhub"
                withCredentials([usernamePassword(credentialsId: 'Admin', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
                sh "docker tag notes-app1 ${env.USERNAME}/notes-app1:latest"
                sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                sh "docker push ${env.USERNAME}/notes-app1:latest"
                }
            }
        }
        
        stage("Deploy the code") {
            steps {
                echo "Deploying the code"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
