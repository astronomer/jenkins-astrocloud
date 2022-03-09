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
           sh 'sudo apt-get install build-essential procps curl file git'
           sh '-c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"'
           sh 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"'
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