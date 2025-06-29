pipeline {
    agent {
        docker {
            image 'python:3.11-slim'
            args '-u root'
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
                    apt-get update
                    apt-get install -y wget curl unzip gnupg apt-transport-https ca-certificates

                    # Install Google Chrome
                    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
                    apt install -y ./google-chrome-stable_current_amd64.deb || apt --fix-broken install -y

                    # Install chromedriver
                    CHROME_VERSION=$(google-chrome --version | grep -oP '\\d+\\.\\d+\\.\\d+')
                    DRIVER_VERSION=$(curl -s https://chromedriver.storage.googleapis.com/LATEST_RELEASE)
                    wget https://chromedriver.storage.googleapis.com/${DRIVER_VERSION}/chromedriver_linux64.zip
                    unzip chromedriver_linux64.zip
                    mv chromedriver /usr/local/bin/
                    chmod +x /usr/local/bin/chromedriver

                    # Install Python dependencies
                    pip install --upgrade pip
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

    post {
        always {
            echo "✅ Build finished. Check console output for test results."
        }
    }
}
