pipeline {
    agent {
        docker {
            image 'selenium/standalone-chrome:latest'
        }
    }
    environment {
        PYTHONUNBUFFERED = '1'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/your-repo.git'  // ✅ Replace with your GitHub repo URL
            }
        }

        stage('Setup Python') {
            steps {
                sh '''
                    apt-get update
                    apt-get install -y python3 python3-pip
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
            echo "Build finished. Check above for test results."
        }
    }
}
