pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/Nifras365/CI-CD-Pipeline-to-Dockerize-application'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t nifras365/new-docker-app:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'my-docker', variable: 'mydocker')]) {
                    script {
                        bat "docker login -u nifras365-p ${samindocker}"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker build -t nifras365/new-docker-app:%BUILD_NUMBER% .'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
