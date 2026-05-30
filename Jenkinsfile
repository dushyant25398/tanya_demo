pipeline {
    agent any

    environment {
        APP_NAME = "tanya_demo"
        PYTHON_FILE = "code"
    }

    options {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code..."
                checkout scm
            }
        }

        stage('Workspace Info') {
            steps {
                echo "Listing files in workspace..."
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Verify Python') {
            steps {
                echo "Checking Python version..."
                sh 'python3 --version'
            }
        }

        stage('Syntax Check') {
            steps {
                echo "Validating Python file syntax..."
                sh 'python3 -m py_compile code'
            }
        }

        stage('Run Application') {
            steps {
                echo "Running the Python script..."
                sh 'python3 code'
            }
        }

        stage('tanya') {
            steps {
                echo "Archiving the source file..."
                archiveArtifacts artifacts: 'code', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully."
        }
        failure {
            echo "Pipeline failed. Check the console output."
        }
        always {
            echo "Cleaning workspace..."
            cleanWs()
        }
    }
}
