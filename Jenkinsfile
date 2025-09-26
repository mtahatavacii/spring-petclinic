pipeline {
    agent any

    environment {
        REGISTRY = "harbor.example.com"
        IMAGE = "harbor.example.com/library/petclinic"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/<senin-github-user>/spring-petclinic.git'
            }
        }

        stage('Build JAR') {
            steps {
                sh "./mvnw clean package -DskipTests"
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                script {
                    docker.withRegistry("https://${env.REGISTRY}", 'harbor-creds') {
                        def app = docker.build("${IMAGE}:${BUILD_NUMBER}")
                        app.push()
                        app.push("latest")
                    }
                }
            }
        }
    }
}
