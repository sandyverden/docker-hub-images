pipeline {
  agent { label 'docker' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  triggers {
    cron('@daily')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -f "Dockerfile-terraform" -t brightbox/terraform:latest .'
        sh 'docker build -f "Dockerfile-cli" -t brightbox/cli:latest .'
      }
    }
    stage('Publish') {
      when {
        branch 'master'
      }
      steps {
	withDockerRegistry([ credentialsId: "6533de7e-17a4-4376-969b-e86bc1e4f903", url: "" ]) {
          sh 'docker push brightbox/terraform:latest'
	  sh 'docker push brightbox/cli:latest'
	}
      }
    }
  }
}
