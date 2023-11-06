pipeline{
    agent any 
    
    tools {
        maven 'Maven_Home'
    }
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/Amitjoshigit/demo-counter-app.git'
                }
            }
        }
        stage('Interation testting') {
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
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-apii'){
                     bat 'mvn clean package sonar:sonar '
                }
                }
            }
        }
        stage('Quality gate status'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-apii'
                }
            }
        }
    }
}
