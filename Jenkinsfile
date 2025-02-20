pipeline {
    agent any

    stages {
            stage('Set Up Python') {
            steps {
                sh 'python3 -m venv venv'  // Create virtual environment
                sh '. venv/bin/activate'   // Activate virtual environment
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest test_main.py'
            }
        }

        stage('Build Artifact') {
            steps {
                sh 'python setup.py sdist'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'dist/*.tar.gz', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build Successful!'
        }
        failure {
            echo '❌ Build Failed! Check logs.'
        }
    }
}
