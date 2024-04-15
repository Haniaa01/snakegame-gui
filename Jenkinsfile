pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            agent {
                docker {
                    image 'python:3.8' // Asumując użycie Python 3.8, dostosuj zgodnie z wymaganiami projektu
                    args '-v $WORKSPACE:/workspace'
                }
            }
            steps {
                dir('/workspace') {
                    sh 'pip install -r requirements.txt'
                }
            }
        }

        stage('Run Tests') {
            agent {
                docker {
                    image 'python:3.8' // Ponowne użycie tego samego obrazu Dockera
                }
            }
            steps {
                dir('/workspace') {
                    sh 'python -m unittest discover' // Zmienione, aby odpowiadało standardowemu sposobowi wywoływania testów w Pythonie
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/*.log', fingerprint: true
            junit '**/test-reports/*.xml' // Tylko jeśli testy generują raporty XML w tym formacie
        }
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
