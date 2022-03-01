node('Built-In') 
{
  stage('ContinuousDownload') 
  {
    git 'https://github.com/kailastambe/maven.git'
  } 
  stage('ContinuousBuild') 
  {
    sh 'mvn package'
  } 
  stage('ContinuousDeployment') 
  {
   echo "I am in deployment phase"
   // sh 'scp /var/lib/jenkins/workspace/Pipeline/webapp/target/webapp.war vagrant@10.10.10.32:/var/lib/tomcat7/webapps/qaenv.war'
  }
  stage('ContinuousTesting') 
  {
    echo " I am in Testing Phase"
    //git 'https://github.com/selenium-saikrishna/TestingOnLinux.git'
    //sh 'java -jar  /var/lib/jenkins/workspace/Pipeline/testing.jar'
  }
  stage('ContinuousDelivery') 
  {
   
   echo " I am in delivery Phase"
   //input message: 'Waiting for approval from DM', submitter: 'Srinivas'
    //sh 'scp /var/lib/jenkins/workspace/Pipeline/webapp/target/webapp.war vagrant@10.10.10.33:/var/lib/tomcat7/webapps/prodenv.war'
  }
  
}
