pipeline {
    agent any

    environment {
        PYTHONUNBUFFERED = '1'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/abdullahs9148/Test-cases-todo.git'
            }
        }
        stage('Setup Python Environment') {
            steps {
                sh '''
                    sudo apt-get update
                    sudo apt-get install -y python3 python3-pip
                    pip3 install pytest selenium
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
    post {
        always {
            echo "Build finished. Check console output for test results."
        }
    }
}
