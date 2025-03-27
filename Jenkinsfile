pipeline {
    agent any
    environment {
        PYTHON_ENV = "python3"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/Yeswanthteja1010/surprisetest.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '${PYTHON_ENV} -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                sh './venv/bin/pytest'
            }
        }
        stage('Build') {
            steps {
                // Add build steps if necessary (e.g., packaging or creating a distribution)
                sh './venv/bin/python setup.py sdist'
            }
        }
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts allowEmptyArchive: true, artifacts: 'dist/*', followSymlinks: false
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
