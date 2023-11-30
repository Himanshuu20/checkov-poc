## Anaplan POC to test the vulnerabilities of terraform scripts using Checkov IAC tool.

### Prerequisite 
    1. Supported IaC Frameworks: Checkov supports various IaC frameworks such as Terraform, Kubernetes, CloudFormation, and more.
       Ensure your IaC framework is supported.
    2. Python: Checkov is written in Python, so you'll need Python installed on your system.
    3. Installation via pip: You can install Checkov using Python's package manager, pip. Use the command pip install checkov to install it.

### Required Action
    Stage Setup in Jenkinsfile: Incorporate a stage within your Jenkinsfile dedicated to running Checkov.
    This stage should contain the necessary commands to execute Checkov against your IaC code.

        pipeline {
            agent any        
            stage('Checkov') {
                 steps {
                     script {
                         docker.image('bridgecrew/checkov:latest').inside("--entrypoint=''") {
                             unstash 'checkov-poc'
                             try {
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
            // Post-build actions, etc.
        }
