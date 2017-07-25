#!groovy
pipeline {
  agent {
    docker {
      image 'widerin/openshift-cli'
        args  '-u 0:0'
    }
  }
  stages {
    stage('Build and Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'occli', passwordVariable: 'octoken', usernameVariable: 'ocproject')]){
          sh "oc login https://api.pro-us-east-1.openshift.com --token=${env.octoken}"
          sh 'oc start-build django-psql-persistent --wait'
        }
      }
    }
  }
}
