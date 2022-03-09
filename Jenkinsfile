pipeline {
 agent any
  environment {
    ASTRONOMER_KEY_ID = "${ASTRONOMER_KEY_ID}"
    ASTRONOMER_KEY_SECRET = "${ASTRONOMER_KEY_SECRET}"
}
   stages {
     stage('Deploy to Astronomer') {
       when {
        expression {
          return env.GIT_BRANCH == "origin/main"
        }
       }
       steps {
         script {
           sh 'export ASTRONOMER_KEY_ID="${ASTRONOMER_KEY_ID}"'
           sh 'export ASTRONOMER_KEY_SECRET="${ASTRONOMER_KEY_SECRET}"'
           sh 'curl https://goreleaserdev.blob.core.windows.net/goreleaser-test-container/releases/v1.3.0/cloud-cli_1.3.0_Linux_x86_64.tar.gz -o astrocloudcli.tar.gz'
           sh 'tar xzf astrocloudcli.tar.gz'
           sh "./astrocloud deploy ${DEPLOYMENT_ID}"
         }
       }
     }
   }
 post {
   always {
     cleanWs()
   }
 }
}