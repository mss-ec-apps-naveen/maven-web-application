node
{

  def mavenHome = tool name: "maven3.8.4"

  stage('Checkout')
 
  {
   git branch: 'development', credentialsId: '8c2bd8df-4164-486d-b861-128e306c4b38', url: 'https://github.com/mss-ec-apps-naveen/maven-web-application.git'

  }
  stage('Build')
  {
  sh "${mavenHome}/bin/mvn clean package"
  }
  
  stage('ExecuteSonarQubeReport')
  {
  sh "${mavenHome}/bin/mvn clean sonar:sonar"
  }
  stage('UploadartipactintoNexus')
  {
  sh "${mavenHome}/bin/mvn clean deploy"
  }
  stage('DepoyAppintoTomcatServer')
  {
  sshagent(['ac863568-de17-43db-8b92-ce7235eef6cd']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.110.107.27:/opt/apache-tomcat-9.0.59/webapps/" 
  }
  
  }
  stage('sendNotification')
  {
   emailext body: '''Build Over


Regards
Naveenkumar''', subject: 'Build Over', to: 'naveenkumar1051@gmail.com'
  }




}
