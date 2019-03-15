# serverless Framework - AWS Python3 Lambda - HelloWorld
Proof of concept using the "serverless" framework to develop an AWS Lambda Project

## Prerequisites

This document assumes you have the following already installed:
- awscli (and you already have your IAM credentials configured)
- python3 (I am using 3.7.2)

You will need an AWS IAM account that has permissions to deploy and invoke AWS Lambda functions.

Finally, this document also assumes you are working on a Mac. I am using a MacBook Pro (5-inch, 2017) running macOS Mojave (10.14.3).

## Quickstart

### Serverless Installation
Install [serverless](https://serverless.com/) as follows:
```
S brew install serverless
```

Check your work:
```
S sls --version

[output]
1.39.0
```

### Create your service
Create a Python3 service as follows:
```
$ sls create --template aws-python3 --path helloWorld

[output]
Serverless: Generating boilerplate...
Serverless: Generating boilerplate in "/Users/bgawryluik/Projects/Training/serverless/serverless-aws-python3-helloworld/helloWorld"
 _______                             __
|   _   .-----.----.--.--.-----.----|  .-----.-----.-----.
|   |___|  -__|   _|  |  |  -__|   _|  |  -__|__ --|__ --|
|____   |_____|__|  \___/|_____|__| |__|_____|_____|_____|
|   |   |             The Serverless Application Framework
|       |                           serverless.com, v1.39.0
 -------'

Serverless: Successfully generated boilerplate for template: "aws-python3"
```

### Run your service locally
Navigate to your service directory:
```
$ cd helloWorld
```  

Invoke your function locally:
```
$ serverless invoke local --function hello

[output]
{
    "statusCode": 200,
    "body": "{\"message\": \"Go Serverless v1.0! Your function executed successfully!\", \"input\": {}}"
}
```  

### Deploy your service to AWS
[*Assuming that your IAM credentials are configured correctly...*]

Ensure that you are still in your service directory:
```
$ pwd
 
[output]
</path/to>/serverless-aws-python3-helloworld/helloWorld
```  

Deploy your function to AWS:
```
$ sls deploy

[output]
Serverless: Packaging service...
Serverless: Excluding development dependencies...
Serverless: Creating Stack...
Serverless: Checking Stack create progress...
.....
Serverless: Stack create finished...
Serverless: Uploading CloudFormation file to S3...
Serverless: Uploading artifacts...
Serverless: Uploading service helloWorld.zip file to S3 (849 B)...
Serverless: Validating template...
Serverless: Updating Stack...
Serverless: Checking Stack update progress...
...............
Serverless: Stack update finished...
Service Information
service: helloWorld
stage: dev
region: us-east-1
stack: helloWorld-dev
resources: 5
api keys:
  None
endpoints:
  None
functions:
  hello: helloWorld-dev-hello
layers:
  None
```

At any time, you can check your work:
```
$ sls info

[output]
Service Information
service: helloWorld
stage: dev
region: us-east-1
stack: helloWorld-dev
resources: 5
api keys:
  None
endpoints:
  None
functions:
  hello: helloWorld-dev-hello
layers:
  None
```

### Run your service on AWS
Invoke your deployed function from your terminal using the following command:

```
$ sls invoke --function hello

[output]
{
    "statusCode": 200,
    "body": "{\"message\": \"Go Serverless v1.0! Your function executed successfully!\", \"input\": {}}"
}
```

### Clean up your service
From the current working directory, delete your function as follows:

```
$ sls remove

[output]
Serverless: Getting all objects in S3 bucket...
Serverless: Removing objects in S3 bucket...
Serverless: Removing Stack...
Serverless: Checking Stack removal progress...
....
Serverless: Stack removal finished...
```  

Check your work:
```
$ sls info

[output]

  Serverless Error ---------------------------------------

  Stack with id helloWorld-dev does not exist

  Get Support --------------------------------------------
     Docs:          docs.serverless.com
     Bugs:          github.com/serverless/serverless/issues
     Issues:        forum.serverless.com

  Your Environment Information -----------------------------
     OS:                     darwin
     Node Version:           11.11.0
     Serverless Version:     1.39.0
```
