pipeline {

  environment {
    registry = "http://192.168.137.150:5000/jenkinssample"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/shohelm/jenkinssample.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build --tag registry + ":latest"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
