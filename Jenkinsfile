def _aws_creds = aws_creds.tokenize()
withEnv(_aws_creds) {
node('master') {
    stage('build') {
         // Checkout the app at the given commit sha from the webhook
        checkout scm
    }

    stage('deploy') {
     sshagent ([aws_creds_key]) {
        sh "echo 'DEPLOYING ${APP_NAME}'"
       sh "ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -b -u ubuntu -i ./inventory app_deploy.yml -e ${APP_NAME}"
       }
    }
  }
}