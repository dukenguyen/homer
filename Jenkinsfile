pipeline {
  agent any
  tools {
    maven 'M3'
  }
  stages {
    stage('Build core') {
      steps {
        build('core')
      }
    }
    stage('Build app') {
      steps {
        sh 'mvn -DskipTests clean install -pl app'
      }
    }
    stage('Build lila/linus/snoopy') {
      parallel {
        stage('Build lila') {
          steps {
            sh 'mvn -DskipTests clean install -pl lila'
          }
        }
        stage('Build linus') {
          steps {
            sh 'mvn -DskipTests clean install -pl linus'
          }
        }
        stage('Build snoopy') {
          steps {
            sh 'mvn -DskipTests clean install -pl snoopy'
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
        sh 'mvn releaser:release'
      }
    }
  }
}

def build(module) {
  sh "mvn -DskipTests clean install -pl $module"
}
