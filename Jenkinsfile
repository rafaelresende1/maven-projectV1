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

    }

            stage ('Deployments'){
 steps {

                build job: 'maven-project'
                    }}
    
        stage('checkstyle') {
            steps {
                sh "mvn clean checkstyle:checkstyle -Dcheckstyle.config.location='https://github.com/rafaelresende1/maven-projectV1.git'"
                checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/checkstyle-result.xml', unHealthy: ''
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
            
        

    
