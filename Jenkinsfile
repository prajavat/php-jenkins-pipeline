pipeline {
    agent any

    stages {
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
	post {
		always {
			mail bcc: '', body: 'Hello, ${JOB_NAME} build ${BUILD_NUMBER} successfully deploy on DevServer. Thankyou.', cc: '', from: 'infra@logilite.com', replyTo: '', subject: '${JOB_NAME} for ${BUILD_NUMBER}', to: 'prajavat@logilite.com'
		}
	} 
}
