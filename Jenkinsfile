pipeline {

  environment {
    dockerimagename = "ramann123/myimage"
    dockerImage = ""
  }

  agent any

  stages {
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhublogin'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }
/*
    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes") 
        }
      }
    }

  }
*/
    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubectl(
            kubernetesContext: 'my-kubernetes-context',
            configs: 'deploymentservice.yml',
            kubeconfigId: 'kubernetes'
          )
        }
      }
    }
}
