pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Pulling latest code from GitHub...'
                git branch: 'main',
                    credentialsId: 'github-creds1',
                    url: 'https://github.com/SagarNajardhane/DevOps_Assingment_7A.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling the application...'
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging JAR...'
                bat 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                bat '''
                taskkill /F /IM java.exe >nul 2>&1
                start /B java -jar target\\*.jar
                '''
            }
        }
    }

    post {
        success {
            echo 'Build, Test and Deployment Successful!'
        }
        failure {
            echo 'Pipeline Failed!'
        }
    }
}
