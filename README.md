# infrastructure

Run the code below for starting the deployment
> aws cloudformation deploy --template-file csye6225-infra.yaml --stack-name test3-cli --profile dev

Run the code below to delete the stack
> aws cloudformation delete-stack --stack-name test3-cli --profile dev