// pipeline {
//     agent any

//     environment {
//         PYTHONUNBUFFERED = '1'
//     }

//     stages {
//         stage('Clone Repository') {
//             steps {
//                 git branch: 'main', url: 'https://github.com/abdullahs9148/Test-cases-todo.git'
//             }
//         }
//         // stage('Setup Python Environment') {
//         //     steps {
//         //         sh '''
//         //             apt-get update
//         //             apt-get install -y python3 python3-pip
//         //             pip3 install pytest selenium
//         //         '''
//         //     }
//         // }

//         stage('Run Selenium Tests') {
//             steps {
//                 sh '''
//                    /home/ubuntu/.local/bin/pytest --maxfail=1 --disable-warnings
//                 '''
//             }
//         }
//     }
//     post {
//         always {
//             echo "Build finished. Check console output for test results."
//         }
//     }
// }
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

        stage('Setup Python Virtual Environment') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install pytest selenium
                '''
            }
        }

        stage('Run Selenium Tests') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest --maxfail=1 --disable-warnings
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

