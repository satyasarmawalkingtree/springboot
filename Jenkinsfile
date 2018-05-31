pipeline {
  agent none
  stages {
    stage('Maven Install') {
      agent {
        docker {
          image 'maven:3.5.0'
        }
      }
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t satyasarma99/test-spring-boot-docker:1.0 .'
      }
    }
     stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'docker-hubPassword', usernameVariable: 'docker-hubUser')]) {
          sh "docker login -u ${env.docker-hubUser} -p ${env.docker-hubPassword}"
          sh 'docker push satyasarma99/test-spring-boot-docker:1.0'
        }
      }
    }
  }
}