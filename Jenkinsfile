pipeline {
    agent any
    stages {
        stage('scm checkout') {
            steps{
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
   } 
}