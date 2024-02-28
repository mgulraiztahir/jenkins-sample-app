pipeline {
    agent any
    environment {
        IMAGE_TAG="${env.BUILD_ID}"
    }
   
    stages {

    // Tests
    stage('Unit Tests') {
      steps{
        script {
          sh 'npm install'
	  sh 'npm test -- --watchAll=false'
        }
      }
    }
        
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          sh 'docker build -t sample_nodejs_application_image:${IMAGE_TAG} .'
        }
      }
    }
   
    stage('Deploy') {
     steps{
        script {
          sh 'docker stop jenkins-with-github-nodejs-cicd-container || true'
          sh 'docker rm jenkins-with-github-nodejs-cicd-container || true'
          sh 'docker run -d -p 80:3000 --name jenkins-with-github-nodejs-cicd-container sample_nodejs_application_image:${IMAGE_TAG}'
          sh 'echo "The Application is available on MachinePublicIP:80"'
        }         
        }
      }      
      
    }
}

