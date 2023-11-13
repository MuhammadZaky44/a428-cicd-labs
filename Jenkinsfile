pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            args '-p 4000:4000'
        }
    }

    stages {
        stage('Build') {
            steps {
                // nodejs(nodeJSInstallationName: 'node10') {
                //     sh 'npm install'
                // }
                sh 'apt install npm'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
               sh './jenkins/scripts/test.sh'
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
