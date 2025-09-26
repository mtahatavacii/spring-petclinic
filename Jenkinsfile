pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/mtahatavacii/spring-petclinic.git', branch: 'main'
            }
        }

        stage('Build with Maven') {
            agent {
                docker {
                    image 'maven:3.9.5-eclipse-temurin-17'
                    args '-v /root/.m2:/root/.m2'  // Maven cache mount
                }
            }
            steps {
                sh "mvn clean package -DskipTests"
            }
        }
    }
}
