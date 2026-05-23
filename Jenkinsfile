pipeline {
    agent any

    environment {
        REGISTRY = "4.231.114.66:5000"
        IMAGE_NAME = "mywebapp"
        TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Lakshminarasimhamura/Azure-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t $REGISTRY/$IMAGE_NAME:$TAG .
                '''
            }
        }

        stage('Push Docker Image to Self Hosted Registry') {
            steps {
                sh '''
                docker push $REGISTRY/$IMAGE_NAME:$TAG
                '''
            }
        }

        stage('Verify Registry') {
            steps {
                sh '''
                curl http://4.231.114.66:5000/v2/_catalog
                '''
            }
        }
    }
}
