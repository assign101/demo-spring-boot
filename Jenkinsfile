pipeline {
  agent any
  stages {
    stage('Checkout'){
      steps{
        checkout scm
       }
      }
    stage('Build Gradle'){
     steps{
       sh './gradlew build'
      }
    }
   
    stage('Docker Build') {
      steps {
        sh 'mkdir -p build/dependency && (cd build/dependency; jar -xf ../libs/*.jar)'
        sh 'docker build -t rajinovat/gs-spring-boot-docker:${env.BUILD_NUMBER} .'
     }
   } 

    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh "docker push rajinovat/gs-spring-boot-docker:${env.BUILD_NUMBER}"
        }
      }
    }

    stage('Docker Remove Image') {
      steps {
        sh "docker rmi rajinovat/gs-spring-boot-docker:${env.BUILD_NUMBER}"
      }
    }
   
}
}
