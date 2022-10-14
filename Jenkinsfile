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
                   sh 'cat docker_pass.txt | docker login -u eddie12345 --password-stdin'
                   sh 'docker push eddie12345/demo-web:DTA'
               } 
            }
    }
}