pipeline {
  agent any
  stages {
    stage('Build Gradle'){
     steps{
        sh 'checkout scm'
        sh 'cd initial'
        sh 'gradlew build && java -jar build/libs/gs-spring-boot-docker-0.1.0.jar'
      }
    }
}
}
