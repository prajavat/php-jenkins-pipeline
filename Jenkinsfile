pipeline {
    agent any

    stages {
        stage('Pre Build') {
            steps {
                git credentialsId: 'ec5f02c4-76ab-44c0-acc0-63d584f0324c', url: 'https://github.com/prajavat/php-jenkins-pipeline.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building Building..'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Deploying....'
            }
        }
    }
}
