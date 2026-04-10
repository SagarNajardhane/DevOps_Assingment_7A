pipeline {
    agent any
    
    tools {
        maven 'Maven'  
    }

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
                /* echo 'Deploying application safely...'
                bat '''
                echo Checking if app is already running...

                for /f "tokens=5" %%a in ('netstat -aon ^| findstr :8081') do (
                    echo Killing process on port 8081...
                    taskkill /PID %%a /F
                )

                echo Starting application...
                start /B java -jar target\\productapp-0.0.1-SNAPSHOT.jar
                ''' */

                /*
                bat '''
                echo Starting app in background...
                java -jar target\\productapp-0.0.1-SNAPSHOT.jar
                ''' */
                bat '''
            echo Killing old app (if running)...
            for /f "tokens=5" %%a in ('netstat -aon ^| findstr :8081') do taskkill /PID %%a /F

            echo Starting app in background (detached)...

            cmd /c "start \"\" java -jar target\\productapp-0.0.1-SNAPSHOT.jar"

            echo Deployment done!
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
