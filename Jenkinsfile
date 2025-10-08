pipeline {
    agent any
    stages {
        stage('scm checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/LohadeDarshan/Nodejs-Project.git'                  
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
        stage('Build Project') {
            steps {
                // Only if project requires build (React, Next.js, etc.)
                sh 'npm run build'
            }
        }
        stage('code deploy') { // will deploy on target machine
            steps {
                sshagent(['DevCICD']) {
                    // Copy project folder to remote machine
                    sh 'scp -o StrictHostKeyChecking=no -r /var/lib/jenkins/workspace/N1 root@10.23.213.210:/home/my-node-app'
                }
            }
        }
        stage('Start Node.js app on remote') {
            steps {
                sshagent(['DevCICD']) {
                    // Start Node.js app on remote machine
                    sh '''
                    ssh -o StrictHostKeyChecking=no root@10.23.213.210 "cd /home/my-node-app/N1 && npm install && npm start &"
                    '''
                }
            }
        }
    }
}