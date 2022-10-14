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
        stage('Push docker images') {
            steps {
               script{
                   sh 'cat docker_pass.txt | docker login -u eddie12345 --password-stdin'
                   sh 'docker push eddie12345/demo-web:DTA'
               } 
            }
        }
        stage('Aqua scanner') {
            steps {
               script{
                   aqua containerRuntime: 'docker', customFlags: '', hideBase: true, hostedImage: 'eddie12345/demo-web:DTA', localImage: '', localToken: '', locationType: 'hosted', notCompliesCmd: '', onDisallowed: 'ignore', policies: '', register: true, registry: 'Docker Hub', scannerPath: '', showNegligible: false, tarFilePath: ''
               } 
            }
        }    
    }
}