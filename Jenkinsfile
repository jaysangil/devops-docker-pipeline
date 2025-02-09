pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "devops-docker-pipeline"
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    checkout([$class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            url: 'https://github.com/jaysangil/devops-docker-pipeline.git',
                            credentialsId: '3295a189-85c9-4080-bfe7-e042c33e79a4'
                        ]]
                    ])
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    sh 'docker run -p 3000:3000 -d $DOCKER_IMAGE'
                }
            }
        }

        stage('Test Application') {
            steps {
                script {
                    sh 'curl http://localhost:3000'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deployment Successful!'
            }
        }
    }

    post {
        failure {
            echo '❌ Build failed! Check logs for details.'
        }
        success {
            echo '✅ Build completed successfully!'
        }
    }
}
