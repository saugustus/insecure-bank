pipeline {
    agent any
    
    stages{
    
    stage('Preparation'){
    def mvnHome
    mvnHome = tool 'localMaven'
    }
     
    stage('Build and Scan'){
            steps {
                bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean compile package/)
                }
            post {
            
                fail{
                    echo 'build fail'
                }
                success {
                    echo 'Now Archiving the war file...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy'){
            steps {
                build job: 'deploy-insecure-bank-app'
            }
        }
    }
}