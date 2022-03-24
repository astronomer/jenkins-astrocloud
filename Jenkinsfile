pipeline {
 agent any
   stages {
     stage('Smoke test') {
       steps {
         script {
           sh 'curl https://goreleaserdev.blob.core.windows.net/goreleaser-test-container/releases/v1.3.2/cloud-cli_1.3.2_Linux_x86_64.tar.gz -o astrocloudcli.tar.gz'
           sh 'tar xzf astrocloudcli.tar.gz'
           sh './astrocloud deploy ${DEPLOYMENT_ID}'
         }
       }
     }
     stage('Deploy to Astronomer') {
       when {
        expression {
          return env.GIT_BRANCH == "origin/main"
        }
       }
       steps {
         script {
           sh 'curl https://goreleaserdev.blob.core.windows.net/goreleaser-test-container/releases/v1.3.2/cloud-cli_1.3.2_Linux_x86_64.tar.gz -o astrocloudcli.tar.gz'
           sh 'tar xzf astrocloudcli.tar.gz'
//            sh 'git status'
//            sh 'git diff'
           sh './astrocloud deploy ${DEPLOYMENT_ID} -f'
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