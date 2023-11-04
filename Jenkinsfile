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
                withSonarQubeEnv(credentialsId: 'sonar-api'){
                     bat 'mvn clean package sonar:sonar '
                }
            }
        }
    }
}
