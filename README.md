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
            
            stages {
                stage('Checkov') {
                    steps {
                        // Assuming Checkov is in the PATH
                        sh 'checkov -d path_to_your_terraform_or_cloudformation_code'
                        // Replace path_to_your_terraform_or_cloudformation_code with your IaC code directory
                    }
                }
                // Other stages in your pipeline
            }
            
            // Post-build actions, etc.
        }

