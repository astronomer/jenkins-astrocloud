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
           sh '$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)'
           sh "brew install astronomer/cloud/astrocloud"
           sh 'astrocloud version'
           sh "astrocloud deploy ${DEPLOYMENT_ID}"
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