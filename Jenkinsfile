pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }

    stages {
        // stage('Git Checkout') {
        //     steps {
        //         script {
        //             git branch: 'main',
        //                 credentialsId: '9b8d225a-a34e-434a-8765-76903368a6c1',
        //                 url: 'https://github.com/Himanshuu20/checkov-poc.git'
        //         }
        //     }
        // }
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
    }
}
