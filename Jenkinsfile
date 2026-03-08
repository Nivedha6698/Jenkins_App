pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK11'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Nivedha6698/Jenkins_App.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

    }

    post {
        success {
            emailext(
                to: 'nivedha6698@gmail.com',
                subject: "Build Success: ${env.JOB_NAME}",
                body: "Build completed successfully"
            )
        }

        failure {
            emailext(
                to: 'nivedha6698@gmail.com',
                subject: "Build Failed: ${env.JOB_NAME}",
                body: "Build failed"
            )
        }
    }
}