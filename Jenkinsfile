pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/shamashaik19/Flask-CI-CD.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t shamashaik19/flask-app:latest .'
            }
        }
        stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push shamashaik19/flask-app:latest'
                }
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name flask-app shamashaik19/flask-app:latest'
            }
        }
    }
}

