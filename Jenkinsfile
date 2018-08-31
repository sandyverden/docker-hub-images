pipeline {
  agent { label 'slave_node_01' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  triggers {
    cron('@daily')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -f "Dockerfile-terraform" -t sandyverden/terraform:latest .'
        sh 'docker build -f "Dockerfile-cli" -t sandyverden/cli:latest .'
      }
    }
    stage('Publish') {
      when {
        branch 'master'
      }
      steps {
	withDockerRegistry([ credentialsId: "36839328-5533-49e1-8a52-be13c6ba0b59", url: "" ]) {
          sh 'docker push sandyverden/terraform:latest'
	  sh 'docker push sandyverden/cli:latest'
	}
      }
    }
  }
}
