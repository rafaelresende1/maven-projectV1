pipeline {
    agent any

    triggers {
            pollSCM('* * * * *')
            }
        
    tools {
            maven 'localMaven'
            git 'localGit'
            }

  stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }

 

            stage ('Deployments'){
                steps {

                build job: 'maven-project'
                    }}
    
        stage('checkstyle') {
           step([$class: 'CheckStylePublisher', pattern: 'target/scalastyle-result.xml, target/scala-2.11/scapegoat-report/scapegoat-scalastyle.xml'])
        }
      
}
        
    }
}
    post {
        success {
        sh "echo 'Send mail on success'"
         // mail to:"rafael.resende@outlook.com", subject:"SUCCESS: ${currentBuild.fullDisplayName}", body: "Yay, we passed."
        }
        failure {
        sh "echo 'Send mail on failure'"
         // mail to:"rafael.resende@outlook.com", subject:"FAILURE: ${currentBuild.fullDisplayName}", body: "Boo, we failed."
    }
    }
 }
            
        

    