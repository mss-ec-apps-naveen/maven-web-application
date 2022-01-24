node
 {

def mavenHome = tool name: "maven3.8.3"
stage('CheckoutCode')
 {
git branch: 'development', credentialsId: '1b7d1b24-dfee-413c-8ad2-49cd45ee36be', url: 'https://github.com/mss-ec-apps-naveen/maven-web-application.git'
 }
stage('Build')
 {
sh "${mavenHome}/bin/mvn clean package"

 }
stage('ExecuteSonarQubeReport')
 {
  sh "${mavenHome}/bin/mvn sonar:sonar"
 }
stage('UploadArtifactintoNexus')
 {
  sh "${mavenHome}/bin/mvn clean deploy"

 }

stage('DeployappintoTomcat')
 { 
sshagent(['524e626e-a892-4586-841c-a004dd905aa3']) {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.1.147.179:/opt/apache-tomcat-9.0.56/webapps/"
   
}
 }
stage('SendNotifications'){
emailext body: '''build over

Regards
naveeen''', subject: 'Build over', to: 'naveenkumar1051@gmail.com'
}

}
