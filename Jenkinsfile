pipeline {
  agent any
  stages {
    //stage('Docker Build') {
      //steps {
        //sh "docker build -t kmlaydin/podinfo:${env.BUILD_NUMBER} ."
      //}
    //}
    //stage('Docker Push') {
      //steps {
        //withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          //sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          //sh "docker push kmlaydin/podinfo:${env.BUILD_NUMBER}"
        //}
      //}
    //}
    //stage('Docker Remove Image') {
      //steps {
        //sh "docker rmi kmlaydin/podinfo:${env.BUILD_NUMBER}"
      //}
    //}
    stage('Apply Kubernetes Deployment') {
      steps {
          withKubeConfig([credentialsId: 'kube-config']) {
          sh 'cat nginx-deploy.yaml' 
             //sed "s/{{BUILD_NUMBER}}/$BUILD_NUMBER/g" | kubectl apply -f -'
          sh 'kubectl apply -f nginx-deploy.yaml'
        }
      }
    }
  }
post {
    success {
      slackSend(message: "Pipeline is successfully completed.")
    }
    failure {
      slackSend(message: "Pipeline failed. Please check the logs.")
    }
  }
}
