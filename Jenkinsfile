pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'java'
        }
     stages {

        stage ('Clone') {
             steps {
                 git url: "https://github.com/kohbah/sprintboot.git"
            }
        }
         

       stage ('Build') {
            steps {
                sh 'mvn clean package' 
            }
       }
         
        stage ('Build docker image') {
            steps {
                script {
                    docker.build('877510168756.dkr.ecr.us-east-1.amazonaws.com/backend/dev:latest')
                }
            }
        }
         
       stage ('ecr login') {
            steps {
                script {
                    sh "/usr/local/bin/aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 877510168756.dkr.ecr.us-east-1.amazonaws.com"
                }
            }
        }  

        stage ('publish ') {
            steps {
                script {
                     sh "docker push 877510168756.dkr.ecr.us-east-1.amazonaws.com/backend/dev:latest"
                    }        
                }
            }
        }
         
     post
        {
            always
            {
                sh "docker rmi 877510168756.dkr.ecr.us-east-1.amazonaws.com/backend/dev:latest"
            }
        }            
    }
