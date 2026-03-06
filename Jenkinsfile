pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "rachana/springboot-devops-app:latest"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Rachana1472/springboot-devops1.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Docker Run') {
            steps {
                sh "docker run -d -p 8082:8081 ${DOCKER_IMAGE}"
            }
        }
    }

    post {
        success { echo 'Pipeline executed successfully ✅' }
        failure { echo 'Pipeline failed ❌' }
    }
}
