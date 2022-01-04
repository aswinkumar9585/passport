pipeline{
   agent {
    docker {
      image 'maven:3.6.3-jdk-11'
      args '-v /root/.m2:/root/.m2'
    }
  }
  stages {
      stage("Maven Build"){
          steps{
              sh 'mvn -B -DskipTests clean package'
          }
      }
      
     stage("Build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('sonarpassport') {
                sh 'java -version'
                sh 'mvn clean package sonar:sonar'
              }
            }
          }
    
  }
        post {  
         always {  
             echo 'This will always run'  
         }  
         success {   
            echo "========Deploying executed successfully========"
             mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER}  <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: 'aswinkumar6493@gmail.com', mimeType: 'text/html', replyTo: '', subject: "success: Project name -> ${env.JOB_NAME}", to: "aswinkumar6493@gmail.com";
           
         }  
         failure {  
             mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: 'aswinkumar6493@gmail.com', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "aswinkumar6493@gmail.com";  
         }  
         unstable {  
             echo 'This will run only if the run was marked as unstable'  
         }  
         changed {  
             echo 'This will run only if the state of the Pipeline has changed'  
             echo 'For example, if the Pipeline was previously failing but is now successful'  
         }  
     }
     
  
        
     
    
  }

           
