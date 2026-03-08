pipeline {
    agent any


    environment {
        RECIPIENTS = 'nivedha6698@gmail.com'
    }

    stages {

        stage('Clone Repository') {
            steps {
                echo "🔹 Stage 1: Cloning the GitHub repository..."
                git branch: 'main', url: 'https://github.com/Nivedha6698/Jenkins_App.git', credentialsId: 'githubtoken'
                echo "Repository cloned successfully."
            }
        }

        stage('Build & Package') {
            steps {
                echo "🔹 Stage 2: Building the project with Maven..."
                sh 'mvn clean package'
                echo "Maven build and package completed."
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo "🔹 Stage 3: Archiving build artifacts..."
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                echo "Artifacts archived successfully."
            }
        }

        stage('Run Application') {
            steps {
                echo "🔹 Stage 4: Running the application..."
                sh 'java -cp target/classes HelloWorld'
                echo "Application ran successfully."
            }
        }
    }

    post {
        success {
            echo "Build succeeded! Sending success email..."
            emailext(
                to: "${env.RECIPIENTS}",
                subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build completed successfully! \nCheck Jenkins job: ${env.BUILD_URL}"
            )
        }

        failure {
            echo "Build failed! Sending failure email..."
            emailext(
                to: "${env.RECIPIENTS}",
                subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build failed! \nCheck Jenkins job: ${env.BUILD_URL}"
            )
        }
    }
}