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
           sh '"$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"'
           sh 'test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)'
           sh 'test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)'
           sh 'test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile'
           sh 'echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile'
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