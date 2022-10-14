pipeline {
    agent any
    stages {
        stage('Build docker image') {
            steps {
               script{
                   sh 'docker build -t eddie12345/demo-web:DTA .' 
               }
            }
        }
    }
}