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
        stage('Push docker images')
            steps {
               script{
                   sh 'docker login -u eddie12345 -p "e9?I(-yHYkx|:J\N"'
                   sh 'docker push eddie12345/demo-web:DTA'
               } 
            }
    }
}