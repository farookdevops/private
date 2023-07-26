node{
def mavenHome = tool name: 'maven3.9.3'
echo "The job name is: ${env.JOB_NAME}"
echo "The build number is: ${env.BUILD_NUMBER}"
//checkout code from SCM
stage('Checkout-code'){
    git branch: 'main', credentialsId: '6a169fe1-9e37-40a4-9d0c-20cebb2ad057', url: 'https://github.com/farookdevops/private.git' 
}
//Build the war application using Maven
stage('Build the code with maven'){
 sh "$mavenHome/bin/mvn clean package"
        
    }
//Deploy to Nexus    
stage('deploy artifacts on Nexus'){
 sh "$mavenHome/bin/mvn deploy"
}
//Deploy to tomcat
stage('Deploy-app-to-tomcat'){
  sshagent(['6c196018-4f45-4ac7-857c-27e36526b79f']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war  ec2-user@13.233.179.197:/opt/apache-tomcat-9.0.78/webapps"
}
}

}
