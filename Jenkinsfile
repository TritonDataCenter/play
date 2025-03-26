/*
 * This Source Code Form is subject to the terms of the Mozilla Public
 * License, v. 2.0. If a copy of the MPL was not distributed with this
 * file, You can obtain one at http://mozilla.org/MPL/2.0/.
 */

/*
 * Copyright 2022 Joyent, Inc.
 * Copyright 2025 MNX Cloud, Inc.
 */

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
        stage('reclean') {
            steps{
                sh('git clean -fdx')
            }
        }
        stage('build') {
            steps{
                sh('''
make print-BRANCH
make print-STAMP
''')
            }
        }
    }

    post {
        always {
            joySlackNotifications()
        }
    }
}
