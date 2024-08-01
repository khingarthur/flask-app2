pipeline {
    agent any 

     options {
        timeout(time: 10, unit: 'MINUTES')
     }
    environment {
    DOCKERHUB_CREDENTIALS = credentials('Dockerhub-pat2')
    APP_NAME = "khingarthur/myflaskapp"
    }
    stages { 
        stage('SCM Checkout') {
            steps{
           git branch: 'main', url: 'https://github.com/khingarthur/flask-app2.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t $APP_NAME:v1.RELEASE .'
            }
        }
        stage('login to dockerhub') {
            steps{
               sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push $APP_NAME:v1.RELEASE'
            }
        }    
    }
}

