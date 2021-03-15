pipeline {
  agent any
          
  stages {        

     stage('Cloning the Project') {
         steps {
             script {
        try{        
            def cause = currentBuild.getBuildCauses('hudson.model.Cause$UserIdCause')
            git 'https://github.com/Bharat2912/sample-app-task.git'
        }
        catch(Exception e) {
          echo "FAILED ${e}"
          currentBuild.result = 'FAILURE'
          throw e
        } }
} }    
        
    stage('Install dependencies') {
  //       slackSend (color: '#FFFF00', message: "Installing dependencies : Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' " , channel: "jenkins" )
      steps {
        sh 'npm install'
      }
    }   
    stage('build-code') {
    //     slackSend (color: '#FFFF00', message: "building-code : Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' " , channel: "jenkins" )        
      steps {
         sh 'npm run build'
      }
    }   
    stage('replace-code') {
      //   slackSend (color: '#FFFF00', message: "replacing-code : Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' " , channel: "jenkins" )        
      steps {
         sh 'tar -czf - ./ | ssh server "tar -C {server-path} -xzf -"'
      }
    }          
  }
}       

