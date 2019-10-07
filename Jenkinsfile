node{
       stage('SCM Checkout') {
           git credentialsId: 'ec5f02c4-76ab-44c0-acc0-63d584f0324c', url: 'https://github.com/prajavat/php-jenkins-pipeline.git'
       }
       stage('Deploy On Dev-Server') {
           sshagent(['192be36e-6db0-49b3-ba61-cbffbf84d5bd']) {
               sh "scp -r -o StrictHostKeyChecking=no * ubuntu@192.168.1.70:/var/www/html/"
           }
       }
       stage ('Build Status') {
           echo "Im not going to fail"
           currentBuild.result = 'SUCCESS'
       } catch (Exception err) {
           currentBuild.result = 'FAILURE'
       }
       stage('Send Notification') {
           emailext body: 'Job $JOB_NAME $BUILD_NUMBER number is ${currentBuild.result}', subject: '$JOB_NAME Status', to: 'prajavat@logilite.com'
       }
}