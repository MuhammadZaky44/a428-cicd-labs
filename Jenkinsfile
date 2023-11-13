pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 4000:4000'
        }
    }
    
    tools {nodejs 'node10'}

    stages {
        stage('Cat') {
            steps {
                sh 'cat Jenkinsfile'
            }
        }
        // stage('Build') {
        //     steps {
        //         nodejs(nodeJSInstallationName: 'node10') {
        //             sh 'npm ls react'
        //         }
        //     }
        // }
        stage('Test') {
            steps {
                nodejs(nodeJSInstallationName: 'node10') {
                    sh './jenkins/scripts/test.sh'
               }
            }
        }

        // stage('Manual Approval') {
        //     steps {
        //         input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)' 
        //     }
        // }
        stage('Deploy') { 
            steps {
                nodejs(nodeJSInstallationName: 'node10') {
                    sh './jenkins/scripts/deliver.sh' 
                    // sleep(time: 1, unit: 'MINUTES')
                    input message: 'Done using the React App?'
                    sh './jenkins/scripts/kill.sh'
               }
            }
        }
    }
}
