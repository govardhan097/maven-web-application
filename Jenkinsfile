node
{
def mavenhome = tool name: "maven3.6.3"
stage('checkoutcode')
{
git branch: 'development', credentialsId: '31b47bc8-2071-4fed-b35e-11f6d02b5573', url: 'https://github.com/govardhan097/maven-web-application.git'
}

stage('build')
{
sh "${mavenhome}/bin/mvn clean package"
}

stage('execute sonarqube report')
{
sh "${mavenhome}/bin/mvn sonar:sonar"
}
stage('upload artifacts in to nexus')
{
sh "${mavenhome}/bin/mvn deploy"
}
stage('deploy app to tomcat')
{
sshagent(['f3212970-3a76-4fd0-b5c2-c3bcbeb87bb3']) 
{
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.126.250.116:/opt/apache-tomcat-9.0.43/webapps/"
}
}
stage('send email notification')
{
mail bcc: '', body: '''build over 

regrads,
govardhan reddy''', cc: '', from: '', replyTo: '', subject: 'build over', to: 'govardhan097@gmail.com'
}
}
