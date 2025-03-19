
pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'  // Change to your preferred region
        INSTANCE_TYPE = 't2.micro'
        AMI_ID = 'ami-0e1bed4f06a3b463d'  // Replace with a valid AMI ID for your region
        KEY_NAME = 'your-key-pair'  // Replace with your EC2 key pair name
        SECURITY_GROUP = 'sg-09e7ad5da636819cb'  // Replace with a valid security group
        SUBNET_ID = 'subnet-031b43c9db2793a81'  // Replace with a valid subnet ID
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/akylgit/test.git'  // Replace with your GitHub repo URL
            }
        }

        stage('Launch EC2 Instance') {
            environment {
                AWS_ACCESS_KEY_ID = credentials('aws-access-key')  
                AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')  
            }
            steps {
                script {
                    sh """
                        aws ec2 run-instances --region $AWS_REGION \
                            --image-id $AMI_ID \
                            --instance-type $INSTANCE_TYPE \
                            --key-name $KEY_NAME \
                            --security-group-ids $SECURITY_GROUP \
                            --subnet-id $SUBNET_ID \
                            --associate-public-ip-address \
                            --count 1
                    """
                }
            }
        }
    }
}
