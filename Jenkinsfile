pipeline {
  agent any
  stages {
    stage('Checkout'){
        checkout scm
      }
    stage('Build Gradle'){
     steps{
        sh '''export GRADLE_USER_HOME=/home/gradle/.gradle
              gradle build && java -jar build/libs/gs-spring-boot-docker-0.1.0.jar'''
      }
    }
}
}
