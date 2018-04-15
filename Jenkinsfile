@@ -1,22 +1,75 @@
pipeline {
    agent any
 
    tools {
        maven 'localMaven'
            }
    pipeline {
        agent any
    
    //    parameters {
       //     string(name: 'tomcat_dev', defaultValue: 'http://localhost:8090/', description: 'Staging Server')
      //      }
        
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



      stage ('Analysis') {
        def mvnHome = tool 'localMaven'
 
        sh "${mvnHome}/bin/mvn -batch-mode -V -U -e checkstyle:checkstyle pmd:pmd pmd:cpd findbugs:findbugs spotbugs:spotbugs"
 
        def checkstyle = scanForIssues tool: [$class: 'CheckStyle'], pattern: '**/target/checkstyle-result.xml'
        publishIssues issues:[checkstyle]
    
        def pmd = scanForIssues tool: [$class: 'Pmd'], pattern: '**/target/pmd.xml'
        publishIssues issues:[pmd]
         
        def cpd = scanForIssues tool: [$class: 'Cpd'], pattern: '**/target/cpd.xml'
        publishIssues issues:[cpd]
         
        def findbugs = scanForIssues tool: [$class: 'FindBugs'], pattern: '**/target/findbugsXml.xml'
        publishIssues issues:[findbugs]
 
        def spotbugs = scanForIssues tool: [$class: 'SpotBugs'], pattern: '**/target/spotbugsXml.xml'
        publishIssues issues:[spotbugs]
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
            
        

    