pipeline {
 agent any
   stages {
     stage('Deploy to Astronomer') {
       when {
        expression {
          return env.GIT_BRANCH == "origin/main"
        }
       }
       steps {
         script {
           brew install astronomer/cloud/astrocloud
           astrocloud deploy $DEPLOYMENT_ID
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