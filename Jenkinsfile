pipeline {
    agent any


    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                dir("my-app") {
                sh "docker build -t ${params.IMAGE_NAME} ."
            }
        }
        }

        stage('Remove Old Container') {
            steps {
                sh """
                docker rm -f ${params.CONTAINER_NAME} || true
                """
            }
        }

        stage('Run Container') {
            steps {
                sh "docker run -d -p 5001:5001 --name ${params.CONTAINER_NAME} ${params.IMAGE_NAME}"
            }
        }
    }
}

