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
                    withCredentials([string(credentialsId: 'password', variable: 'dockerpwd')]) {
                        def password = env.dockerpwd
                    bat "docker login -u reickii -p ${password}"}
                    bat 'docker push reickii/devops-integration'
                }
            }
        }
    }
}