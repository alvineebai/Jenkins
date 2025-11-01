pipeline {
    agent any

    stages {
        stage('codescan') {
            steps {
                sh 'trivy fs . -o result.html'
                
            }
        }
        stage('dockerImageBuild') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 337909783644.dkr.ecr.us-east-1.amazonaws.com'
                sh 'docker build -t jenkins-repo . .'
                sh 'docker tag jenkins-repo:latest 337909783644.dkr.ecr.us-east-1.amazonaws.com/jenkins-repo:latest'
                sh 'docker push 337909783644.dkr.ecr.us-east-1.amazonaws.com/jenkins-repo:latest'
            }
        }
        stage('checkcontainer') {
            steps {
                sh 'docker ps -a'
                
            }
        }
    }
    
}
