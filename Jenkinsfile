@Library('jenkins-joylib@v1.0.8') _

pipeline {
    agent {
        label 'platform:true && image_ver:21.4.0 && pkgsrc_arch:x86_64 && ' +
        'dram:16gb && !virt:kvm && fs:pcfs && fs:ufs && jenkins_agent:3'
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '30'))
        timestamps()
    }

    stages {
        stage('check') {
            steps{
                sh('make check')
            }
        }
    }

    post {
        always {
            joySlackNotifications(channel: 'jenkins', comment: 'play message')
            slackSend(channel: 'smartos', color: 'good', message: 'another play message')
        }
    }
}
