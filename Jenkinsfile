pipeline {
  agent any
  tools {
    maven 'M3'
  }
  stages {
    stage('Build homer') {
      steps {
        build('.')
      }
    }
    stage('Build core') {
      steps {
        build('core')
      }
    }
    stage('Build app') {
      steps {
        build('app')
      }
    }
    stage('Build lila/linus/snoopy') {
      parallel {
        stage('Build lila') {
          steps {
            build('lila')
          }
        }
        stage('Build linus') {
          steps {
            build('linus')
          }
        }
        stage('Build snoopy') {
          steps {
            build('snoopy')
          }
        }
      } 
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Publish') {
      steps {
        sh 'mvn releaser:release -DskipTests'
      }
    }
  }
}

def build(module) {
  sh "mvn -DskipTests clean install -pl $module"
}
