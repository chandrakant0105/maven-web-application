node
{
    def mavenHome = tool name: "maven3.8.5"
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
    stage('CheckoutCode'){
        git branch: 'development', credentialsId: '325cb2e7-5ffa-4fa3-9947-1ff3717ee678', url: 'https://github.com/chandrakant0105/maven-web-application.git'
    }
    
   stage('build'){
       sh "${mavenHome}/bin/mvn clean package"
   }
    
   stage('exicute sonarqube report'){
       sh "${mavenHome}/bin/mvn sonar:sonar"
   } 
  stage('upload artifacts into nexus'){
      sh "${mavenHome}/bin/mvn deploy"
  }  

    stage('send email notification'){
        emailext body: '''build over..

regards,
chandrakant sahoo''', subject: 'build over', to: 'chandrakantasahoo76@gmail.com'
    }
}
