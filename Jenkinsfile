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
           sh "brew install astronomer/cloud/astrocloud"
           sh "astrocloud deploy $DEPLOYMENT_ID"
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