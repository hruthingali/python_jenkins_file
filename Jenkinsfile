pipeline {
    agent any

    stages {
       stage('Set Up Python') {
            steps {
                sh 'python3 -m venv venv'  // Create virtual environment
                sh 'echo "source venv/bin/activate" >> ~/.bashrc'  // Ensure venv is sourced
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '. venv/bin/activate && python -m ensurepip --default-pip'  // Ensure pip is available
                sh '. venv/bin/activate && pip install --upgrade pip setuptools wheel'  // Upgrade pip
                sh '. venv/bin/activate && pip install -r requirements.txt'  // Install dependencies
            }
        }

        stage('Run Tests') {
            steps {
                sh '. venv/bin/activate && pytest test_main.py'  // Run tests
            }
        }

        stage('Build Artifact') {
            steps {
                sh '. venv/bin/activate && python setup.py sdist'  // Build Python package
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
