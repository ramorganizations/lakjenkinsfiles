node
{
def mavenHome = tool name: "maven3.6.3"
 properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '4', daysToKeepStr: '', numToKeepStr: '5')), parameters([choice(choices: ['master', 'development', 'qa ', 'uat'], description: '', name: 'BranchName')]), pipelineTriggers([pollSCM('* * * * *')])])

stage('Getting code from GitHub')
{
    git branch: 'development', credentialsId: '68635b32-2285-4317-9c23-7ed2e70ba9cb', url: 'https://github.com/ramorganizations/maven-web-application.git'
}
stage('Build')
{
  sh "${mavenHome}/bin/mvn clean package"  
}
stage('Execute SonarQube Report')
{
    sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('Store Artifacts into nexus Repo')
{
    sh "${mavenHome}/bin/mvn deploy"
}
stage('Deploy Application into Tomcat Server')
{
    sshagent(['5eceb255-fd2b-448e-a1f2-73c292a2af7a']) {
    sh " scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.175.135.250:/opt/apache-tomcat-9.0.37/webapps"
}
}
stage('Send Email Notification')
{
    emailext body: '''build is successful..

Regards,
lakshmi.''', subject: 'build is successful', to: 'bhuludondeti@gmail.com'
}
}
