node{
    
    def mavenhome = tool name: "maven3.8.5"

stage('checkout code')
{
 git credentialsId: '9a8dbbb1-cb2a-4cec-9a6b-2e895458537c', url: 'https://github.com/viswareddy17/maven-web-application.git'
}

stage('build')
{
 sh "${mavenhome}/bin/mvn clean package" 
}
stage('sonarqube report')
{
sh "${mavenhome}/bin/mvn clean sonar:sonar"
}
stage('uploadartifactsintonexus')
{
sh "${mavenhome}/bin/mvn clean deploy"
}
stage('DeployappintoTomcatServer')
{
sshagent(['7c926bb3-3c50-47c0-9478-b7bbd5791a41'])
{
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.0.127.206:/opt/apache-tomcat-9.0.62/webapps"   
}
}
stage('tosendEmailNotifications')
{
emailext body: '''Regards,
Devops Team
THIS''', subject: 'Build is Over', to: 'baddipalliviswa17@gmail.com'
}

}
