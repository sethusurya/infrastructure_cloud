# infrastructure

Run the code below for starting the deployment
> aws cloudformation deploy --template-file csye6225-infra.yaml --stack-name test3-cli --profile dev

Run the code below to delete the stack
> aws cloudformation delete-stack --stack-name test3-cli --profile dev


Run the code below to create stack with ec2
> aws cloudformation create-stack --stack-name appstack --template-body file://csye6225-infra.yaml --parameters ParameterKey=VpcCIDR,ParameterValue="10.1.0.0/16" ParameterKey=SubnetCidrBlock1,ParameterValue="10.1.1.0/24" ParameterKey=SubnetCidrBlock2,ParameterValue="10.1.2.0/24" ParameterKey=SubnetCidrBlock3,ParameterValue="10.1.3.0/24" ParameterKey=AmiId,ParameterValue="ami-0d97c92948d354176" --region us-east-1 --profile=dev

Run the code below to delete the above created stack
> aws cloudformation delete-stack --stack-name appstack --region us-east-1 --profile=dev