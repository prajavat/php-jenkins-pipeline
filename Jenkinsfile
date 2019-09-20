pipeline {
    agent any

    stages {
        stage('Pre Build') {
            steps {
                sh 'sudo apt-get install apache2'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Deploying....'
            }
        }
    }
}