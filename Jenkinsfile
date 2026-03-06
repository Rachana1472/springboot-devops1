pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "rachana/springboot-devops-app:latest"
    }

    stages {
        stage('Build') {
            steps {
                // Use system Maven and Java from PATH
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Run Unit Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                bat "docker build -t ${DOCKER_IMAGE} ."
            }
        }

        stage('Docker Run') {
            steps {
                bat "docker run -d -p 8082:8081 ${DOCKER_IMAGE}"
            }
        }
    }

    post {
        success { echo 'Pipeline executed successfully ✅' }
        failure { echo 'Pipeline failed ❌' }
    }
}
