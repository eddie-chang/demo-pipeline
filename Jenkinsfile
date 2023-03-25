pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script{
                   sh 'docker build --no-cache -t eddie12345/log4j-demo -f demo-cve/Dockerfile demo-cve' 
               }
            }
        }
        stage('Prisma Cloud Scan Docker Image') {
            steps {
                // Scan the image
                prismaCloudScanImage ca: '',
                cert: '',
                dockerAddress: 'unix:///var/run/docker.sock',
                image: 'eddie12345/log4j-demo*',
                key: '',
                logLevel: 'info',
                podmanPath: '',
                // The project field below is only applicable if you are using Prisma Cloud Compute Edition and have set up projects (multiple consoles) on Prisma Cloud.
                project: '',
                resultsFile: 'prisma-cloud-scan-results.json',
                ignoreImageBuildTime:true
            }
        }
    }
    post {
        always {
            // The post section lets you run the publish step regardless of the scan results
            prismaCloudPublish resultsFilePattern: 'prisma-cloud-scan-results.json'
        }
    }
}