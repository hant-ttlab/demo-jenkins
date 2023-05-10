pipeline {
  agent any

  environment {
    GREEN_NAMESPACE = "${ECR_REPOSITORY}-prod-green"
  }

  stages {
    stage('build') {
      steps {
        echo 'building image'
      }
    }
  }
}

