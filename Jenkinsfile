def _aws_creds = aws_creds.tokenize()
withEnv(_aws_creds) {
node('master') {
    stage('build') {
         // Checkout the app at the given commit sha from the webhook
        checkout scm
    }

    stage('deploy') {
     sshagent ([aws_creds_key]) {
        sh "ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -b -u ubuntu -i ./inventory deploy_clock.yml"
        sh "echo 'DEPLOYING CLOCK'"
       }
    }
  }
}