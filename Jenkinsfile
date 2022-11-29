pipeline {
agent any
    stages {

        stage('login') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 941066304506.dkr.ecr.us-east-1.amazonaws.com'
            }
        }

        stage('build') {
            steps {
                sh 'docker build -t test-repo .'
            }
        }

      stage('tag') {
            steps {
                sh 'docker tag test-repo:latest 941066304506.dkr.ecr.us-east-1.amazonaws.com/test-repo:latest'
            }
        }

         stage('push') {
            steps {
                sh 'docker push 941066304506.dkr.ecr.us-east-1.amazonaws.com/test-repo:latest'
            }
        } 
       stage('deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        } 
    }
        

    }