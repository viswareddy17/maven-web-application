node{
    def mavenHome = tool name: "maven 3.8.2"
    stage('checkOutCode')
    {
    git branch: 'development', credentialsId: '49c0ae50-e2a8-493b-bc97-e2d4d60c1225', url: 'https://github.com/viswareddy17/maven-web-application.git'
    }
    stage('toTriggerBuildPackage')
    {
    sh "${mavenHome}/bin/mvn clean package"
    }
    stage('toExceuteTheSonarQubeReport')
    {
    sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('toUploadArtifactsIntoNexus')
    {
    sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('to deploy the war files into tomcat server')
    {
        sshagent(['45e8bf26-32e6-4fe9-ae20-5355db56a430']) {
     sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.108.196.234:/opt/apache-tomcat-9.0.52/webapps/"
}
    }
    stage('to Send Out Email Notification')
    {
    emailext body: '''Build is over...
    
Thanks&Regards,
Mithun technologies''', subject: 'Build is over pipeline script ......', to: 'baddipalliviswa17@gmail.com'
    }
}
