pipeline {
    agent any
    parameters {
        string(name: 'Artifact URL', defaultValue: '', description: 'Provide the URL of the plugin Artifacts')
        string(name: 'S3 Bucket Name', defaultValue: '', description: 'Provide the S3 Bucket Name')
        choice(name: 'Plugin Type', choices: ['intellij', 'eclipse', 'jenkins'], description: 'Select the Plugin Type')
        }

stages{

  stage('CheckOutCode'){
    steps{
    git branch: 'development', credentialsId: 'Git_Cred', url: 'https://github.com/VijayPersistent/maven-web-application.git'
	
	}
  }
  
  stage('Build'){
  steps{
  sh  "mvn clean package"
  }
  }
   stage('Upload to AWS S3') {
              steps {
                  withAWS(region:'us-east-1',credentials:'aws_cred') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'app.py', bucket:'vijay-jenkins-to-s3')
                  }
              }
         }
}
}
