pipeline {
    agent any
 
    tools {
        maven 'C:\Users\rafae\OneDrive\Documents\JENKINS\apache-maven-3.5.3'
        git 'localGit'
    }


stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}