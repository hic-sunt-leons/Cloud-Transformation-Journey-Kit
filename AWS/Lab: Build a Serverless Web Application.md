
Before starting the Lab, it is recommended to create a IAM User to the Lab and dont use your ROOT User account. Navigate to the IAM Service and just go through the steps to create a new IAM User. It is pretty intuitive. 
Helpful link if needed not really needed. [create-iam-users](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#create-iam-users)

In order to clone repo that you create, you need to generate a username and password in order clone the repo to your local machine.
[Setup for HTTPS users using Git credentials](https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-gc.html?icmpid=docs_acc_console_connect_np)

The AWS CLI need to be setup already to your IAM User that you created. The CLI will be used to copy static files from public accessible AWS S3 service to your local GIT repo. Refer to this for assistance: [cli-configure-files](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)

To get the creditals to setup your CLI, go to the IAM service and select the IAM User and select the "Security credentials" tab.  In the Access key section, click "Create access key" and ue the generated keys for setting up the AWS CLI to your AWS account.

[Lab: build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito](https://aws.amazon.com/getting-started/hands-on/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/)



Help information if you need it:

>Information  
>If you messup and enter in the wrong creditials when trying to Clone the repo that was created created. Go to the following link update the creditals.
>[remove-credentials-from-git](https://stackoverflow.com/questions/15381198/remove-credentials-from-git)

