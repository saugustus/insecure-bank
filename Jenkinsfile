pipeline {
    agent any
    stages{
        stage('build'){
            steps {
                sh 'mvn clean compile package'
            }
            post {
                success {
                    echo 'Now Archiving the war file...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('deploy'){
            steps {
                build job: 'deploy-insecure-bank-app'
            }
        }
    }
}