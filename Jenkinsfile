pipeline {
    agent any
    environment {
        IMAGE_TAG="${env.BUILD_ID}"
    }
   
    stages {

    // Tests
    //stage('Unit Tests') {
      //steps{
        //script {
          //sh 'npm install'
	  //sh 'npm test -- --watchAll=false'
        //}
      //}
    //}
        
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          sh 'docker images -a -q'
          sh 'docker build -t docker_jenkins_image:${IMAGE_TAG} .'
        }
      }
    }
   
    stage('Deploy') {
     steps{
        script {
          sh 'docker stop $(docker ps -a -q) || true'
          sh 'docker rm -v $(docker ps --filter status=exited -q) || true'
          sh 'docker run -d -p 80:3000 --name jenkins-container docker_jenkins_image:${IMAGE_TAG}'
          sh 'echo "The Application is available on MachinePublicIP:80"'
        }         
        }
      }      
      
    }
}

