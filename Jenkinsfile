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
}
}
