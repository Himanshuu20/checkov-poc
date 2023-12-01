## Anaplan POC to test the vulnerabilities of terraform scripts files using Checkov IAC tool.

### Prerequisite 
    1. Checkov is a static code analysis tool for scanning infrastructure as code (IaC) files and to test the vulnerabilities of terraform scripts files.
    2. Python: Checkov is written in Python, so you'll need Python installed on your system.
    3. Installation via pip: You can install Checkov using Python's package manager, pip. Use the command pip install checkov to install it.

### Execution
    Whenever any changes pushed to the repo. Jenkinsfile pipeline will triggers and generate the test result report according to the changes.

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

### Result

![TESTRESULT](/home/himanshu.sagar/Pictures/result.png)