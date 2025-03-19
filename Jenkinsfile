pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        INSTANCE_TYPE = 't2.micro'
        AMI_ID = 'ami-0e1bed4f06a3b463d'
        KEY_NAME = 'your-key-pair'
        SECURITY_GROUP = 'sg-09e7ad5da636819cb'
        SUBNET_ID = 'subnet-031b43c9db2793a81'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/akylgit/test.git'
            }
        }

        stage('Launch EC2 Instance') {
            steps {
                withCredentials([aws(credentialsId: 'aws-credentials', region: "${AWS_REGION}")]) {
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
