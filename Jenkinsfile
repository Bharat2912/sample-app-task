pipeline {
  agent any
          
  stages {
     stage('remove-old-code') {
         steps {
        sh 'rm -rf * .env'
     } }          
    stage('Cloning Git') {
//slackSend (color: '#FFFF00', message: "cloning-projetc : Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' " , channel: "jenkins" )
      steps {
        git 'https://github.com/Bharat2912/sample-app-task.git'
      }
    }
        
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

