pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp-image"
        CONTAINER_NAME = "myapp-container"
    }

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                dir("my-app") {
                sh "docker build -t $IMAGE_NAME ."
            }
        }
        }

        stage('Remove Old Container') {
            steps {
                sh """
                docker rm -f $CONTAINER_NAME || true
                """
            }
        }

        stage('Run Container') {
            steps {
                sh "docker run -d -p 5001:5001 --name $CONTAINER_NAME $IMAGE_NAME"
            }
        }
    }
}

