pipeline {
    agent any

    environment {
        PYTHONUNBUFFERED = '1'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/abdullahs9148/Test-cases-todo.git'
            }
        }

        stage('Kill Existing Chrome Instances') {
            steps {
                sh '''
                    pkill chrome || true
                '''
            }
        }

        stage('Run Selenium Tests') {
            steps {
                sh '''
                    /var/lib/jenkins/.local/bin/pytest --maxfail=1 --disable-warnings
                '''
            }
        }
    }

    post {
        always {
            echo "✅ Build finished. Check console output for results."
        }
    }
}
