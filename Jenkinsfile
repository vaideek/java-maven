pipeline {
  agent any
  stages {
    stage('code') {
      steps {
        git(url: 'https://github.com/vaideek/java-maven.git', branch: 'main')
      }
    }

    stage('build') {
      steps {
        sh 'mvn clean install'
      }
    }

    stage('deploy') {
      steps {
        sshagent(ignoreMissing: true)
      }
    }

  }
}