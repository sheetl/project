pipeline {
    agent any

    stages {
        stage('Pre Cleanup Workspace') {
            steps {
                script {
                    sh label: '', script: 'docker system prune -f > /dev/null 2>&1'
                    cleanWs()
                }
            }
        }
        stage('Checkout SCM') {
            steps {
                script {
                   git credentialsId: 'githubcredentials', url: 'https://github.com/sheetalrajan99/Assessment.git'
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                   sh label: '', script: 'docker build -t nodeapplication .'
                }
            }
        }
        stage('Docker Push to ECR') {
            steps {
                script {
                    docker.withRegistry('https://691665429187.dkr.ecr.us-west-2.amazonaws.com/nodeapplication:latest', 'ecr:us-west-2:AWSCredentials') {
                        docker.image('nodeapplication').push('latest')
                    }
                }
            }
        }
        stage('Post Cleanup Workspace') {
            steps {
                script {
                    sh label: '', script: 'docker system prune -f > /dev/null 2>&1'
                    cleanWs()
                }
            }
        }
    }
}