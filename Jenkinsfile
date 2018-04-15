pipeline {
    agent any
 
    parameters {
         string(name: 'tomcat_dev', defaultValue: 'http://localhost:8090/', description: 'Staging Server')
        }
    
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
                sh 'mvn clean package'
                    }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }

        }

  stage('Static Code Analysis'){
          steps {
                checkout scm
                sh "echo 'Run Static Code Analysis'"
                }

        stage ('Deployments'){


            build job: 'maven-project'
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
        }
    

