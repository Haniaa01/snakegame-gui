pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            agent { label 'docker-capable' } // agent musi mieć zainstalowanego Dockera
            steps {
                script {
                    docker.image('python:3.8').inside('-v $WORKSPACE:/workspace') {
                        sh 'pip install -r requirements.txt'
                        sh 'python -m unittest discover'
                    }
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/*.log', fingerprint: true
            junit '**/test-reports/*.xml'
        }
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
