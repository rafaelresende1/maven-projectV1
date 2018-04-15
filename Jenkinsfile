pipeline {
    agent any
 
    tools {
        maven 'localMaven'
        git 'localGit'
    }


stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            
        }
    }
}
