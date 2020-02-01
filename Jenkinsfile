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
       sh './gradlew build && java -jar build/libs/gs-spring-boot-docker-0.1.0.jar'
      }
    }
}
}
