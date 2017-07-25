#!groovy
pipeline {
    agent none
    stages {
       stage('Build') {
           agent {
               docker {
                   image 'widerin/openshift-cli'
                   args  '-u 0:0'
               }
           }
           steps {
               withCredentials([usernamePassword(credentialsId: 'occli', passwordVariable: 'octoken', usernameVariable: 'ocproject')]){
               sh "oc login https://api.pro-us-east-1.openshift.com --token=\'${env.octoken}\'"
               echo "building now....."
             }
           }
       }
       stage('Deploy') {
           agent {
               docker {
                   image 'widerin/openshift-cli'
                   args  '-u 0:0'
               }
           }
           steps {
               withCredentials([usernamePassword(credentialsId: 'occli', passwordVariable: 'octoken', usernameVariable: 'ocproject')]){
               sh "oc login https://api.pro-us-east-1.openshift.com --token='${env.octoken}'"
               sh 'oc deploy django-psql-persistent --latest'
           }
         }
      }
  }
}
