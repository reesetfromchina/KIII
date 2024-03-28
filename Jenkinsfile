pipeline {
  agent any
  stages {
    stage('Clone repository') {
      steps {
        checkout scm
      }
    }

    stage('Build image') {
      steps {
        script {
          app = docker.build("reesetfromchina/KIII")
        }

      }
    }

    stage('Push image') {
      steps {
        script {
          withDockerRegistry([credentialsId: 'navipro', url: 'https://registry.hub.docker.com']) {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
          }
        }

      }
    }

  }
}