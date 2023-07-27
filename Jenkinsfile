pipeline{
 agent any

 properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: '']])

 properties([[$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([githubPush()])])
 tools{
     maven "maven3.9.3"
 }
 
 stages{
  stage('CheckoutCode'){
  steps{
   git branch: 'development', url: 'https://github.com/farookdevops/private.git'
  }
  }
  stage('Build'){
   steps{
       sh "mvn clean package"
   }
  }
  stage('DeployToNexus'){
    steps{
        sh "mvn deploy"
    }
  }
  stage('DeployToTomcat'){
   steps{
   sshagent(['151d54cf-90f2-4cd1-a897-2bb33d5994aa']) {
     sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.234.202.101:/opt/apache-tomcat-9.0.78/webapps"
                                          }
                         }
                }
}
}
