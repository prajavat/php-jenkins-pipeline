emailNotifications = 'prajavat@logilite.com'
notificationSent    = false

def sendNotification(buildChanged)
{
    if (notificationSent)
    {
        return
    }
    notificationSent = true

    if (currentBuild.currentResult == 'SUCCESS')
    {
        // notify users when the build is back to normal
        mail to: emailNotifications,
            subject: "Build fixed: ${currentBuild.fullDisplayName}",
            body: "The build is back to normal ${env.BUILD_URL}"
    }
    else if ((currentBuild.currentResult == 'FAILURE') && buildChanged)
    {
        // notify users when the Pipeline first fails
        mail to: emailNotifications,
            subject: "Build failed: ${currentBuild.fullDisplayName}",
            body: "Something went wrong with ${env.BUILD_URL}"
    }
    else if ((currentBuild.currentResult == 'FAILURE'))
    {
        // notify users when they check into a broken build
        mail to: emailNotifications,
            subject: "Build failed (again): ${currentBuild.fullDisplayName}",
            body: "Something is still wrong with ${env.BUILD_URL}"
    }
}

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
                    sh "scp -r -o StrictHostKeyChecking=no * ubuntu@192.168.1.700:/var/www/html/"
                }
            }
        }
    }
    post {
        changed {
            sendNotification buildChanged:true
        }
        failure {
            sendNotification buildChanged:false
        }
    }
}
// node{
//        stage('SCM Checkout') {
//            git credentialsId: 'ec5f02c4-76ab-44c0-acc0-63d584f0324c', url: 'https://github.com/prajavat/php-jenkins-pipeline.git'
//        }
//        stage('Deploy On Dev-Server') {
//            sshagent(['192be36e-6db0-49b3-ba61-cbffbf84d5bd']) {
//                sh "scp -r -o StrictHostKeyChecking=no * ubuntu@192.168.1.70:/var/www/html/"
//            }
//        }
//        stage('Send Notification') {
//            emailext body: 'Job $JOB_NAME Build number: $BUILD_NUMBER is ', subject: '$JOB_NAME Status', to: 'prajavat@logilite.com'
//        }
// }