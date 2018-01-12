pipeline {
  agent any
  tools {
    maven 'M3'
  }
  stages {
    stage('Build core') {
      steps {
        sh 'mvn -DskipTests clean package -pl core'
      }
    }
    stage('Build app') {
      steps {
        sh 'mvn -DskipTests clean package -pl app'
      }
    }
    stage('Build lila/linus/snoopy') {
      parallel {
        stage('Build lila') {
          steps {
            sh 'mvn -DskipTests clean package -pl lila'
          }
        }
        stage('Build linus') {
          steps {
            sh 'mvn -DskipTests clean package -pl linus'
          }
        }
        stage('Build snoopy') {
          steps {
            sh 'mvn -DskipTests clean package -pl snoopy'
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
