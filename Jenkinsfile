pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ritobrotoram-ai/demo-spring-boot.git'
            }
        }
        stage('Build & Test') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean test'
            }
        }
        stage('Package JAR') {
            steps {
                sh './mvnw package -DskipTests'
            }
        }
        stage('Deploy') {
            steps {
#                // Replace this with your actual deployment step (e.g., Docker, SCP, or systemd restart)
#                echo 'Build complete! Ready to deploy target/*.jar'
                sh 'sudo systemctl restart springboot-app'
            }
        }
    }
    post {
        always {
            // Archives the built JAR file inside Jenkins after every run
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}
