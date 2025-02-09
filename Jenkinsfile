pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "devops-docker-pipeline"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/jaysangil/devops-docker-pipeline.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -p 3000:3000 -d $DOCKER_IMAGE'
            }
        }

        stage('Test Application') {
            steps {
                sh 'curl http://localhost:3000'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deployment Successful!'
            }
        }
    }
}
