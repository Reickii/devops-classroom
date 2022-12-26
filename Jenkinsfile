pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Reickii/devops-classroom']]])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t reickii/devops-integration .'
                }
            }
        }
        stage('push image to hub'){
            steps{
                script{
                    bat 'docker login -u reickii -p '
                    bat 'docker push reickii/devops-integration'
                }
            }
        }
    }
}