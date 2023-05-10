pipeline {
  agent any

  environment {
    GREEN_NAMESPACE = "${ECR_REPOSITORY}-prod-green"
  }

  stages {
    stage('build') {
      steps {
        // script {
        //   env.GREEN_TRAFFIC = sh(script:"kubectl get ingress ${ECR_REPOSITORY} --namespace ${GREEN_NAMESPACE} -o json | jq '.metadata.annotations[\"nginx.ingress.kubernetes.io/canary-weight\"]' -r", returnStdout: true).trim()
        // }
        sh 'printf "Current Green Traffic: ${GREEN_TRAFFIC}%%\\nNew Green Traffic: ${GREEN_TRAFFIC_PERCENT}%%"'
        
        // Wait for input
        timeout(time: 1, unit: "HOURS") {
          input message: 'Confirm adjust traffic?', ok: 'Yes, adjust traffic'
        }

        // Set traffic
        sh "helm upgrade ${ECR_REPOSITORY} ./chart/ --install --create-namespace --wait --debug --namespace ${GREEN_NAMESPACE} --reuse-values --set ingress.canaryWeight=${GREEN_TRAFFIC_PERCENT}"
      }
    }
  }
}

