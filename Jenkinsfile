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
                script {
                    try {
                        timeout(time: 10, unit: 'MINUTES') {
                            sh '''
                                echo "=== Starting dependency installation ==="
                                apt-get update -o Acquire::ForceIPv4=true
                                apt-get install -y --no-install-recommends \
                                  wget curl unzip gnupg \
                            apt-transport-https ca-certificates
                        
                        # Check what's running
                        ps aux
                        
                        # Install Chrome with more robust commands
                        wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add -
                        echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list
                        apt-get update
                        apt-get install -y google-chrome-stable
                        
                        # Install chromedriver
                        CHROME_VERSION=$(google-chrome --version | awk '{print $3}')
                        DRIVER_VERSION=$(curl -s https://chromedriver.storage.googleapis.com/LATEST_RELEASE_$CHROME_VERSION)
                        wget -N https://chromedriver.storage.googleapis.com/$DRIVER_VERSION/chromedriver_linux64.zip
                        unzip chromedriver_linux64.zip
                        mv chromedriver /usr/local/bin/
                        chmod +x /usr/local/bin/chromedriver
                        
                        # Python dependencies
                        pip install --no-cache-dir --upgrade pip
                        pip install pytest selenium
                    '''
                }
             } catch (err) {
                echo "Dependency installation failed: ${err}"
                sh 'ps aux'  // Show what processes are running
                sh 'lsof'    // Show open files
                error("Dependency installation timed out")
            }
        }
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
