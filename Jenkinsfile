pipeline {
    agent any

    tools {
        maven 'Maven_Home'
    }

    stages {
        stage('Git Checkout') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/Amitjoshigit/demo-counter-app.git'
                }
            }
        }

        stage('Interation testing') {
            steps {
                script {
                    bat "mvn verify -DskiUnitTests"
                }
            }
        }

        stage('Maven Build') {
            steps {
                script {
                    bat "mvn clean install"
                }
            }
        }

        stage('Static code analysis') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-apii') {
                        bat 'mvn clean package sonar:sonar'
                    }
                }
            }
        }

        stage('uploading war'){
            steps{
                script {

                nexusArtifactUploader artifacts: [
                    [artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'nexus-auth', groupId: 'com.example', nexusUrl: 'localhost:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'demo-app', version: '1.0.0'
                }
            }
        }
    }
}
