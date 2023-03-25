pipeline {
    agent any
    
    environment {
        PRISMA_API_URL='https://api.sg.prismacloud.io'
        PC_USER='fd88a3ff-b980-4d0a-951e-6627f65dd826'
        PC_PASSWORD='JTaxZqE/cMxMtJnsjrbnMJ3fVG4='
    }
    
    stages {
        stage('Checkout') {
          steps {
              git branch: 'main', url: ''https://github.com/eddie-chang/demo-pipeline.git''
              stash includes: '**/*', name: 'source'
          }
        }
        stage('Checkov') {
            steps {
                withCredentials([string(credentialsId: 'PC_USER', variable: 'pc_user'),string(credentialsId: 'PC_PASSWORD', variable: 'pc_password')]) {
                    script {
                        docker.image('bridgecrew/checkov:latest').inside("--entrypoint=''") {
                          unstash 'source'
                          try {
                              sh 'checkov -d . --use-enforcement-rules -o cli -o junitxml --output-file-path console,results.xml --bc-api-key \$\{pc_user}::\$\{pc_password} --repo-id  eddie-chang/demo-pipeline --branch main'
                              junit skipPublishingChecks: true, testResults: 'results.xml'
                          } catch (err) {
                              junit skipPublishingChecks: true, testResults: 'results.xml'
                              throw err
                          }
                        }
                    }
                }
            }
        }
    }
    options {
        preserveStashes()
        timestamps()
    }
}