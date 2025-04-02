pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Install Firebase Tools
                sh 'npm install -g firebase-tools'
            }
        }
        
        stage('Testing') {
            steps {
                withCredentials([string(credentialsId: 'firebase-token', variable: 'FIREBASE_TOKEN')]) {
                    sh 'firebase use testing --token $FIREBASE_TOKEN'
                    sh 'firebase deploy --token $FIREBASE_TOKEN'
                }
            }
        }
        
        stage('Staging') {
            steps {
                withCredentials([string(credentialsId: 'firebase-token', variable: 'FIREBASE_TOKEN')]) {
                    sh 'firebase use staging --token $FIREBASE_TOKEN'
                    sh 'firebase deploy --token $FIREBASE_TOKEN'
                }
            }
        }
        
        stage('Production') {
            steps {
                withCredentials([string(credentialsId: 'firebase-token', variable: 'FIREBASE_TOKEN')]) {
                    sh 'firebase use production --token $FIREBASE_TOKEN'
                    sh 'firebase deploy --token $FIREBASE_TOKEN'
                }
            }
        }
    }
}
