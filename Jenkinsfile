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

        stage('Run Selenium Tests') {
            steps {
                sh '''
                    /home/ubuntu/.local/bin/pytest --maxfail=1 --disable-warnings
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
