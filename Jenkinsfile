@Library('jenkins-joylib@v1.0.8') _

pipeline {
    agent {
        label joyCommonLabels(platform: true, image_ver: '21.4.0', pi:'20210826T002459Z'
        )
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '30'))
        timestamps()
    }

    stages {
        stage('check') {
            agent {
                node {
                    label 'platform:true && image_ver:21.4.0 && pkgsrc_arch:x86_64 && ' +
                    'dram:16gb && !virt:kvm && fs:pcfs && fs:ufs && jenkins_agent:3'
                }
            }
            steps{
                sh('make check')
            }
        }
    }

    post {
        always {
            joySlackNotifications(channel: 'jenkins', comment: 'play message')
            joySlackNotifications(channel: 'smartos', comment: 'play message')
        }
    }
}
