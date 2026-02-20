@Library('shared') _ 
pipeline {
    agent any
    
  
    
    stages {
        
     
        
        stage('code') {
            steps {
                echo 'cloning code from github'
                // git url: "https://github.com/saiyedin786/TravelMemory_prashant.git",branch: "main"
                script{
                    clone("https://github.com/saiyedin786/TravelMemory_prashant.git","main")
                }
                echo 'cloning complete'
            }
        }
        stage('Building backend') {
            steps {
                echo 'Build start'
                sh 'docker build -t saiyedin786/travelmememory-prashant:backend01  ./backend'
                echo 'Build complete'
                 echo 'push start start'
                withCredentials([usernamePassword('credentialsId': 'dockerHubCred',
                usernameVariable: 'dockerHubUser',
                passwordVariable: 'dockerHubPass')]){
                
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/travelmememory-prashant:backend01"
                }
                
                echo 'push end'
            }
        }
         stage('Building frontend') {
            steps {
                echo 'Build start'
                sh 'docker build -t saiyedin786/travelmememory-prashant:frontend01  ./frontend'
                echo 'Build complete'
                
                  echo 'push start start'
                withCredentials([usernamePassword('credentialsId': 'dockerHubCred',
                usernameVariable: 'dockerHubUser',
                passwordVariable: 'dockerHubPass')]){
                
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/travelmememory-prashant:frontend01"
                }
                
                echo 'push end'
                
            }
        }
         stage('Deploy') {
            steps {
                echo 'Deploy start'
                sh "docker compose down && docker compose up -d"
                echo 'Deploy end'
            }
        }
        
    }
}
