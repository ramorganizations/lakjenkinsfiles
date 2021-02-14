node
{
    def mavenHome = tool name: 'maven3.6.3'
    
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('')])])
    
    stage('Checkout')
    {
      git branch: 'development', credentialsId: '8c619a76-32a1-45b7-af0e-cc3e03782886', url: 'https://github.com/ramorganizations/maven-web-application.git'
    }
    stage('Build')
    {
       sh  "${mavenHome}/bin/mvn clean package"
    }
    stage('ExecuteSonarQubeReportReport')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('storeAtrtifactsinto/nexus')
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage('DeployAppintoTomcatServer')
    {
       sshagent(['914fb055-2fa8-426c-9b6f-e44b97feb22f']) {
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.132.215.125:/opt/apache-tomcat-9.0.41/webapps"
        }  
    }
    stage('SendEmail/notificstion')
    {
        emailext body: '''build is success


        regards.
        lak''', subject: 'build is success', to: 'bhulakshmidondeti@gmail.com'
    }
    
}
