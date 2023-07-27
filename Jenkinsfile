//node {
//    docker.image('node:16-buster-slim').inside('-p 3000:3000'){
//        stage('Build'){
//           sh 'npm install'
//        }
//        stage('Test'){
//           sh './jenkins/scripts/test.sh' 
//        }
//        triggers {
//            pollSCM('H/2 * * * *')
//        }
//   }
//}

pipeline {
    agent {
        docker {
            image 'node:16-buster-slim' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh' 
            }
        }
        stage('Manual Approval') { 
            steps {
                input message: 'Lanjutkan ke tahap Deploy?'
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                // input message: 'Sudah selesai menggunakan react app? (Klik "proceed" untuk mengakhiri)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
    triggers {
        pollSCM('H/2 * * * *')
    }
}