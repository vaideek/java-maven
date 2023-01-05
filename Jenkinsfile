pipeline {
  agent any
  stages {
    stage('code') {
      steps {
        sh 'echo $whoami'
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
        sshagent(['deploy_user'])
           sh 'scp -o StrictHostKeyChecking=no java-maven_main/target/myshuttledev.war slave@20.112.15.64:/opt/tomcat/webapps'
           
      }
    }

  }
}
