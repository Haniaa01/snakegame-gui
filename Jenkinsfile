pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Haniaa01/snakegame-gui'
            }
        }

        stage('Build') {
            steps {
                sh 'docker-compose up --build'
            }
        }

    }

    post {
        success {
            echo 'Budowa zakończona sukcesem!'
        }
        failure {
            echo 'Budowa nie powiodła się.'
        }
    }
}
