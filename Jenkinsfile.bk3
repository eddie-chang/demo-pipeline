pipeline {
    agent any
    stages {
        stage('Build docker image') {
            steps {
               script{
                   sh 'docker build --no-cache -t eddie12345/log4j-demo:DTA -f demo-cve/Dockerfile demo-cve' 
               }
            }
        }
        stage('Aqua scanner') {
            steps {
               script{
                   aqua containerRuntime: 'docker', customFlags: '', hideBase: false, hostedImage: '', localImage: 'eddie12345/log4j-demo:DTA', localToken: '', locationType: 'local', notCompliesCmd: '', onDisallowed: 'fail', policies: '', register: false, registry: '', scannerPath: '', showNegligible: false, tarFilePath: ''
               } 
            }
        }
        stage('Push docker images') {
            steps {
               script{
                   sh 'cat docker_pass.txt | docker login -u eddie12345 --password-stdin'
                   sh 'docker push eddie12345/log4j-demo:DTA'
               } 
            }
        }    
    }
}