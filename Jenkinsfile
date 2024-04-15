pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:3.8'
                    args '-v /home:/home'
                }
            }
            steps {
                sh 'pip install -r requirements.txt'
                sh 'python setup.py build'
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'python:3.8'
                    args '-v /home:/home'
                }
            }
            steps {
                sh 'python -m unittest discover'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/*.log', fingerprint: true
        }
    }
}

