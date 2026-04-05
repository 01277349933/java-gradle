// Jenkinsfile — Java + Gradle CI/CD Pipeline
// CodeAlpha DevOps Internship — Task 3

pipeline {
    agent any

    tools {
        jdk 'JDK-17'
    }

    environment {
        APP_NAME = 'codealpha-java-app'
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Checking out source code..."
                checkout scm
            }
        }

        stage('Build Info') {
            steps {
                sh './gradlew buildInfo'
            }
        }

        stage('Compile') {
            steps {
                echo "Compiling Java source..."
                sh './gradlew compileJava'
            }
        }

        stage('Test') {
            steps {
                echo "Running unit tests..."
                sh './gradlew test'
            }
            post {
                always {
                    junit 'build/test-results/test/*.xml'
                }
            }
        }

        stage('Build JAR') {
            steps {
                echo "Building JAR artifact..."
                sh './gradlew build'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
                }
            }
        }

        stage('Run App') {
            steps {
                echo "Running the application..."
                sh './gradlew run'
            }
        }
    }

    post {
        success {
            echo "✅ Build and tests passed! JAR is ready for deployment."
        }
        failure {
            echo "❌ Build failed. Check the logs above."
        }
    }
}
