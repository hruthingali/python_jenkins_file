pipeline {

agent any

stages {

stage('Clone Repository') {

steps {

git url:'https://github.com/hruthingali/python_jenkins.git',branch:'main'

}

}

stage('Install Dependencies') {

steps {

sh 'pip install -r requirements.txt'

}

}

stage('Run Tests') {

steps {

sh 'pytest tests/'

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

}
