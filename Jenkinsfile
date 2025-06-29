pipeline {
    agent {
        docker {
            image 'python:3.11-slim'   // ✅ Docker container with Python pre-installed
        }
    }

    environment {
        PYTHONUNBUFFERED = '1'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/abdullahs9148/Test-cases-todo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    pip install pytest selenium
                '''
            }
        }

        stage('Run Selenium Tests') {
            steps {
                sh '''
                    pytest --maxfail=1 --disable-warnings
                '''
            }
        }
    }
    }
