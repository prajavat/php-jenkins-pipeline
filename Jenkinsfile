pipeline {
    agent any

    stages {
        stage('Send Notification') {
            emailext body: 'Thank you!', subject: 'Hello', to: 'prajavat@logilite.com'
        }
        stage('SCM Checkout') {
            steps {
                git credentialsId: 'ec5f02c4-76ab-44c0-acc0-63d584f0324c', url: 'https://github.com/prajavat/php-jenkins-pipeline.git'
            }
        }
        stage('Deploy On Dev-Server') {
            steps {
                sshagent(['192be36e-6db0-49b3-ba61-cbffbf84d5bd']) {
					sh "scp -r -o StrictHostKeyChecking=no * ubuntu@192.168.1.70:/var/www/html/"
				}
            }
        }
    }
}

// node{
//        stage('Send Notification') {
//            emailext body: 'Thank you!', subject: 'Hello', to: 'prajavat@logilite.com'
//        }
//        stage('SCM Checkout') {
//            git credentialsId: 'ec5f02c4-76ab-44c0-acc0-63d584f0324c', url: 'https://github.com/prajavat/php-jenkins-pipeline.git'
//        }
//        stage('Deploy On Dev-Server') {
//            sshagent(['192be36e-6db0-49b3-ba61-cbffbf84d5bd']) {
//                sh "scp -r -o StrictHostKeyChecking=no * ubuntu@192.168.1.70:/var/www/html/"
//            }
//        }
// }