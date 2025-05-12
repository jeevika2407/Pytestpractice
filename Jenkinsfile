pipeline {
    agent any

    environment {
        PYTHONPATH = "${env.WORKSPACE}"
    }

    tools {
        // Optional: define Python if set up in Jenkins tools
        // python 'Python 3.x'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Clones the repo (if using with Git SCM)
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Run Specific Pytest File') {
            steps {
                dir('python_selenium') {
                    bat 'pytest alert.py --maxfail=1 --disable-warnings -v'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        failure {
            echo 'Tests failed.'
        }
        success {
            echo 'Tests passed successfully.'
        }
    }
}
