pipeline {
    agent any  // Use any available agent
    environment {
        PATH ="/opt/tomcat/bin:$PATH"     
    }

    tools {
        maven 'maven'  // Ensure this matches the name configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/s43861999/first-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'  // Run Maven build
            }
        }
        stage('connect to server') {
            steps {
              sshagent(['tomcat']) {

                 sh "ls -l $WORKSPACE/target/"
                 sh "pwd"
                 sh "scp -o StrictHostKeyChecking=no $WORKSPACE/target/devopsnew.war tomcat@ec2-13-219-73-117.compute-1.amazonaws.com:/opt/tomcat/webapps"


                }
       
               }
         }        
         
    }
}
