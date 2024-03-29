# IAC using AWS CloudFormation

```Name: Sethusuryateja Pagolu, NUID - 002122149, Email - pagolu.s@northeastern.edu```
# infrastructure

Run the code below for starting the deployment
> aws cloudformation deploy --template-file csye6225-infra.yaml --stack-name test3-cli --profile dev

Run the code below to delete the stack
> aws cloudformation delete-stack --stack-name test3-cli --profile dev


Run the code below to create stack with ec2
> aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yaml --parameters ParameterKey=VpcCIDR,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=AmiId,ParameterValue="ami-0d97c92948d354176" --region us-east-1 --profile=dev

Run the code below to delete the above created stack
> aws cloudformation delete-stack --stack-name appstack --region us-east-1 --profile=dev

<!-- Stack for private subnets and rdb-->
> aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yml --parameters ParameterKey=VPCCidrBlock,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=PrivateSubCidrBlock1,ParameterValue="10.1.4.0/24" ParameterKey=PrivateSubCidrBlock2,ParameterValue="10.1.5.0/24" ParameterKey=PrivateSubCidrBlock3,ParameterValue="10.1.6.0/24" ParameterKey=AmiId,ParameterValue="ami-0c1864d6e14143cf6" --region us-east-1 --profile=dev  --capabilities CAPABILITY_NAMED_IAM

<!-- Set profile and region -->
# Set Profile
> export AWS_PROFILE=prod
> export AWS_REGION=us-east-1 
# Stack with rds and s3
> aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yaml --parameters ParameterKey=VpcCIDR,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=PrivateSubCidrBlock1,ParameterValue="10.1.4.0/24" ParameterKey=PrivateSubCidrBlock2,ParameterValue="10.1.5.0/24" ParameterKey=PrivateSubCidrBlock3,ParameterValue="10.1.6.0/24" ParameterKey=S3BucketName,ParameterValue="sethusurya.dev.csye6225.01" ParameterKey=AmiId,ParameterValue="ami-0247678d613f74cf6" ParameterKey=DomainPrefix,ParameterValue="prod" --region us-east-1 --profile=prod  --capabilities CAPABILITY_NAMED_IAM

# S3 bucket commands
> aws s3 rm s3://sethusurya.dev.csye6225.01 --recursive --profile=dev
> aws s3api delete-bucket --bucket sethusurya.dev.csye6225.01 --region us-east-1 --profile=dev

# IMPORTANT POINT
For a production profile, it is necessary to give DomainPrefix which is existing in hosting zones, currently prod.sethusurya.me. is available in hosted zones in production and dev.sethusurya.me is available in dev account. so the domain prefix would be either prod or dev. giving the wrong domain prefix will fail creating the stack

# for new org
> aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yaml --parameters ParameterKey=VpcCIDR,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=PrivateSubCidrBlock1,ParameterValue="10.1.4.0/24" ParameterKey=PrivateSubCidrBlock2,ParameterValue="10.1.5.0/24" ParameterKey=PrivateSubCidrBlock3,ParameterValue="10.1.6.0/24" ParameterKey=S3BucketName,ParameterValue="sethusurya.production.csye6225.02" ParameterKey=AmiId,ParameterValue="ami-09355e4d0ee6bd5ba" ParameterKey=DomainPrefix,ParameterValue="production" ParameterKey=DomainName,ParameterValue="sethusurya.com." ParameterKey=SENDGRIDAPI,ParameterValue="api-key-here" --region us-east-1 --profile=production  --capabilities CAPABILITY_NAMED_IAM

# CodeDeploy Stack
aws cloudformation create-stack --stack-name codedeploystack --template-body file://ci-cd-infra.yaml --parameters ParameterKey=CodeDeployBucketName,ParameterValue="codedeploy.sethusurya.com" --region us-east-1 --profile=production --capabilities CAPABILITY_NAMED_IAM

# For importing ssl from namecheap to aws certificate manager
aws iam upload-server-certificate --server-certificate-name certificate_object_name --certificate-body file://*path to your certificate file* --private-key file://*path to your private key file* --certificate-chain file://*path to your CA-bundle file* --profile=production
