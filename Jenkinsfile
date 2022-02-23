pipeline {
  environment {
    imagename = "chinmay927-image"
    registryCredential = '927chinmay-aws'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/chinmay9279/927C7Assignment.git', branch: 'master', credentialsId: 'docker-jenkins-chinmay929'])

      }
    }
    stage('Build and Push') {
      steps{
        script {
          docker.withRegistry('https://655621747571.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:927chinmay-aws') {
            dockerImage = docker.build('chinmay927-assignment')
			dockerImage.push('latest')
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
	    sh "ssh -i /home/ubuntu/927courseAssignment.pem ubuntu@10.0.10.13"
			docker.withRegistry( 'https://655621747571.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:927chinmay-aws' ) {
			docker.pull()
			docker.build('chinmay927-assignment')
			docker.withRun('-p 8080:8080')
            		}
      }
    }
  }
}
