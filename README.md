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

    Test Result (12 failures / ±0)
    /terraform/main.tf.aws_security_group.allow_web.[NONE][CKV_AWS_260] Ensure no security groups allow ingress from 0.0.0.0:0 to port 80
    /terraform/main.tf.aws_security_group.allow_web.[NONE][CKV_AWS_23] Ensure every security groups rule has a description
    /terraform/main.tf.aws_instance.web-server.[NONE][CKV_AWS_8] Ensure all data stored in the Launch configuration or instance Elastic Blocks Store is securely encrypted
    /terraform/main.tf.aws_instance.web-server.[NONE][CKV_AWS_126] Ensure that detailed monitoring is enabled for EC2 instances
    /terraform/main.tf.aws_instance.web-server.[NONE][CKV_AWS_135] Ensure that EC2 is EBS optimized
    /terraform/main.tf.aws_instance.web-server.[NONE][CKV_AWS_79] Ensure Instance Metadata Service Version 1 is not enabled
    /terraform/main.tf.aws.default.[NONE][CKV_AWS_41] Ensure no hard coded AWS access key and secret key exists in provider
    /terraform/main.tf.aws_vpc.prod-vpc.[NONE][CKV2_AWS_12] Ensure the default security group of every VPC restricts all traffic
    /terraform/main.tf.aws_instance.web-server.[NONE][CKV2_AWS_41] Ensure an IAM role is attached to EC2 instance
    /terraform/main.tf.aws_vpc.prod-vpc.[NONE][CKV2_AWS_11] Ensure VPC flow logging is enabled in all VPCs
    /terraform/main.tf.aws_eip.one.[NONE][CKV2_AWS_19] Ensure that all EIP addresses allocated to a VPC are attached to EC2 instances
    /terraform/variable.tf.f0132863827315357a36d7523aa3590c973677b9.[NONE][CKV_SECRET_2] AWS Access Key
