pipeline {
  agent {
    dockerfile {
      filename 'tests/Dockerfile'
      # additionalBuildArgs "put additional args"
      args "-u 0"
    }
  }
  environment {
    GOPATH = '/usr/share/go'
  }
  stages {
    stage('Build') {
       steps {
         sh 'go version'
       }
    }
    stage('Test') {
       steps {
         sh './tests/test.sh'
       }
    }
    stage('Deliver for development') {
      when {
        branch 'dev' 
      }
      steps {
        sh 'ansible-playbook -i depoly/inventory/hosts depoly/dev.yml'
      }
    }
    stage('Deploy for production') {
      when {
        tag '*'  
      }
      steps {
        sh 'ansible-playbook -i depoly/inventory/hosts depoly/prod.yml'
      }
    }
  }
}
