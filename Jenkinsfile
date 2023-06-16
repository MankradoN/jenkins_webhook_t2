pipeline {
    agent any
    environment{
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    } 
    stages {
        stage('Initialisation') { 
            steps {
                sh 'docker rm -f $(docker ps -aq) || true'
            }
        }
        stage('Build') { 
            steps {
                sh "chmod +x deploy.sh"
                sh "./deploy.sh" 
            }
        }
        stage('Push') { 
            steps {
                sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"
                echo "Login completed!!"
                sh "docker tag trio-task-mysql:5.7 mankradon/trio-task-mysql:latest"
                sh "docker tag trio-task-flask-app:latest mankradon/trio-task-flask-app:latest"
                sh "docker push mankradon/trio-task-mysql:latest"
                sh "docker push mankradon/trio-task-flask-app:latest"
            }
            }
        }
    }
