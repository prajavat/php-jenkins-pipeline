pipeline{
	agent any

	stages {
		stage('SCM Checkout') {
            steps {
                git credentialsId: 'ec5f02c4-76ab-44c0-acc0-63d584f0324c', url: 'https://github.com/prajavat/php-jenkins-pipeline.git'
            }
		}
        stage('Deploy On DevServer') {
            steps {
                def scpcommand = 'ubuntu@192.168.1.70:/var/www/html/'
				sshagent(['192be36e-6db0-49b3-ba61-cbffbf84d5bd']) {
					ssh "scp -r -o StrictHostKeyChecking=no * ${scpcommand}"
				}
            }
        }
	}
}
