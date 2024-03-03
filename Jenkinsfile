pipeline {
    agent {label "Slave-Docker"} 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-veera')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/sysgeeks4u/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t rnraju/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push rnraju/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
