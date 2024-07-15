pipeline {
    agent any
    
    stages {
        stage('Code') {
            steps {
                echo "Cloning the code"
                git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
            }
        }
        
        stage('Build') {
            steps {
                echo "Building the code"
                sh 'docker build -t my-note-app .'
            }
        }
        
        stage('Push to docker Hub') {
            steps {
                echo "Pushing the code to Docker Hub"
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                    sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        
        stage('Deploy') {
            steps {
                echo "Deploying the code"
                // Add your deployment steps here
                sh "docker-compose down && docker-compose up -d"
               
            }
        }
    }
}
