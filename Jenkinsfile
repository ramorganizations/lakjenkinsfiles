node
{
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: '']])
    def mavenHome = tool name: "maven3.8.1"
    stage('Checkout')
    {
        git branch: 'development', credentialsId: '26beb6b9-b6b7-452e-ada7-355d0bb08cc3', url: 'https://github.com/ramorganizations/maven-web-application.git'
    }
    stage('Build a package')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    /*stage('Generate SonarQube Report')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('Store BuidArtifacts into nexus Repo')
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage('Deploy into Tomcat Server')
    {
        sshagent(['9a1cb013-a4be-4870-ae7e-3013c0bd3a12']) {
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.58.124.180:/opt/apache-tomcat-9.0.46/webapps/"
       }
    }
    stage('Send Email Notification')
    {
        emailext body: '''Build completed successfully.
        Regards,
        lakshmi.''', subject: 'About build', to: 'bhulakshmidondeti@gmail.com'
    }*/
}
