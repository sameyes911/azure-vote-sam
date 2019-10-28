pipeline {
  agent {
    kubernetes {
      yamlFile './podTemplate.yaml'
    }
  }
  stages {
    stage("pull source code"){
        steps {
            git url: 'https://github.com/sameyes911/azure-vote-sam', branch: 'master', credentialsId: "cf748a1ea72c51e5f98f8324059dae4ee355a403"
        }     
    }  
    stage('image build') {
      steps {
        container('docker') {
            //build image
            sh 'docker build -t rancherlbacr.azurecr.io/azure-vote-front:latest ./azure-vote'
            // docker login
            sh 'docker login rancherlbacr.azurecr.io -u rancherlbacr -p c=b5Vc7lhdqkKR7xME0Rqq9pggSrW6KZ'
            // docker image push
            sh 'docker push rancherlbacr.azurecr.io/azure-vote-front:latest'
        }
      }
    }

    stage('trigger deployment') {
        // trigger deployment
        steps {
            build 'azure-vote-front-deployment'
        }
    }
  }
}