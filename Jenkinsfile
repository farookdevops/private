pieline{
agent any 
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: '']])
properties([[$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([githubPush()])])
tools {
maven "maven3.9.3"
}
stages{
  stage('CheckoutCode'){
  steps{
    git branch: 'development', credentialsId: '6a169fe1-9e37-40a4-9d0c-20cebb2ad057', url: 'https://github.com/farookdevops/private.git'
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
    sshagent(['6c196018-4f45-4ac7-857c-27e36526b79f']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@13.234.202.101:/opt/apache-tomcat-9.0.78/webapps"
                                                       }
                         }
                   }
}
}

