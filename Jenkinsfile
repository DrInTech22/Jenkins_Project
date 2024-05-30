#!/usr/bin/env groovy

pipeline {
    agent any
    tools{
        maven 'maven-3'
    }
    stages {
        stage('test') {
            steps {
                script {
                    echo "Testing the application...\n \n \n"
                    sh 'mvn test'
                }
            }
        }
        stage('build jar') {
            steps {
                script {
                    echo "building the application... \n \n \n"
                    sh 'mvn package'
                }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "Deploying the application... \n \n \n"
                    withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                    sh 'docker build -t maestrops/demo-app:1.0 .'
                    sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                    sh 'docker push maestrops/demo-app:1.0' 
                    }
                }
            }
        }
    }
}

