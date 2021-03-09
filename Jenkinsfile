node()
{
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: '']])
    def mavenHome = tool name: "maven3.6.3"
    stage("CheckOut")
    {
        git branch: 'development', credentialsId: 'c7023370-b546-41c8-9a02-f72f784312e4', url: 'https://github.com/ramorganizations/maven-web-application.git'
    }
    stage("Build a Package")
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    /*stage("Generate SonarQubeReport")
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage("Store Aritifacts into Nexus Repo")
    {
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage("Deploy into TomcatServer")
    {
        sshagent(['c4d09e25-1138-4c54-acfa-de553186eaa9']) {
         sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.224.169.54:/opt/apache-tomcat-9.0.41/webapps"
        }
    }
    stage("Send Email Notification")
    { 
        emailext body: 'Build is over..', subject: 'Build Info', to: 'bhulakshmidondeti'
    }*/
}
