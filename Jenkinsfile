pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }

    stages {
        stage('Checkout') {
             steps {
                 git branch: 'main', url: 'https://github.com/Himanshuu20/checkov-poc.git'
                 stash includes: '**/*', name: 'checkov-poc'
             }
         }     
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                failure{
                     echo "checkov build failed"
                }
            }
        }
        stage('Checkov') {
             steps {
                 script {
                     docker.image('bridgecrew/checkov:latest').inside("--entrypoint=''") {
                         unstash 'checkov-poc'
                         try {
                            //--api-key 43ed0ff9-b43a-4034-a20d-a35f8001ec4c
                             sh 'checkov -d . -o cli -o junitxml --output-file-path console,results.xml --repo-id Himanshuu20/checkov-poc --branch main'
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
