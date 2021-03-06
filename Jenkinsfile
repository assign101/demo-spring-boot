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

    stage('Copy Dependencies') {
      steps {
        sh 'mkdir -p build/dependency && cd build/dependency && jar -xf ../libs/*.jar && cd ../../'
     }
   }
   
    stage('Docker Build') {
      steps {

        sh 'docker build --build-arg DEPENDENCY=build/dependency -t rajinovat/gs-spring-boot-docker .'
     }
   } 

    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh "docker push rajinovat/gs-spring-boot-docker"
        }
      }
    }

    stage('Deploy to DEV namespace') {
      steps {
          withKubeConfig([credentialsId: 'kubeconfig']) {
          sh 'cat service.yaml | sed "s/{{ENV}}/dev/g"' 
          sh 'cat deployment.yaml | sed "s/{{BUILD_NUMBER}}/$BUILD_NUMBER/g" | sed "s/{{ENV}}/dev/g" | kubectl apply -f -'
          sh 'kubectl apply -f service.yaml'
        }
      }
  }

    stage('Docker Remove Image') {
      steps {
        sh "docker rmi rajinovat/gs-spring-boot-docker"
      }
    }
   
}
}
