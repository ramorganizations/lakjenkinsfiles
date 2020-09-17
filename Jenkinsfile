node['slaves']
{
 def mavenHome = tool name: "maven 3.6.3"
 properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
stage('CheckOutBuild')
{
git branch: 'development', credentialsId: 'b52e47f8-e9b1-47a8-b8b4-3931abd70f47', url: 'https://github.com/ramorganizations/maven-web-application.git'
}
stage('Build')
{
    sh "${mavenHome}/bin/mvn clean package"
}
/* 
stage('ExecuteSonarQubeReport')
{
    sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('BuildArtifactsReport')
{
    sh "${mavenHome}/bin/mvn deploy"
}
stage('DeployAppintoTomcatServer')
{
sshagent(['c383e4e4-ecef-4292-b8cd-90e52411277c']) 
{
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@100.25.163.228:/opt/apache-tomcat-9.0.37/webapps"
}
}
stage('SendEmailNotifications')
{
emailext body: '''build is done.


regards,
lakshmi.''', subject: 'build done..', to: 'bhuludondet@gmail.com'
}*/

}
