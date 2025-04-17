pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/name/myfirst.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                dir('DockerJenkinsExperiment') {
                    sh 'ls -l'
                    sh 'docker build -t my-docker-webapp .'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8081:80 my-docker-webapp'
            }
        }
    }
}
