pipeline {
  agent { label 'docker' }
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
        sh 'docker push brightbox/terraform:latest'
	sh 'docker push brightbox/cli:latest'
      }
    }
  }
}
