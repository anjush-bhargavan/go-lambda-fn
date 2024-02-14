# go-lambda-fn

# AWS Lambda Function Setup

This repository contains instructions for setting up an AWS Lambda function using the AWS CLI.

## Prerequisites

Before you begin, ensure you have the AWS CLI installed and configured with appropriate permissions.

## Instructions

### Clone the Repository

  ```bash
    git clone https://github.com/anjush-bhargavan/go-lambda-fn.git
    cd go-lambda-fn
```
### Create role

```bash
  aws iam create-role --role-name MyLambdaRole --assume-role-policy-document file://trust-policy.json
```
### Attach trust policy

```bash
  aws iam put-role-policy --role-name MyLambdaRole --policy-name LambdaTrustPolicy --policy-document file://trust-policy.json
```
### Create function

```bash
  aws lambda create-function \
--function-name MyLambdaFunction \
--runtime go1.x \
--role arn:aws:iam::YOUR_AWS_ACCOUNT_ID:role/MyLambdaRole \
--handler lambda_function.lambda_handler \
--zip-file fileb://function.zip
```
### Invoke function

```bash
  aws lambda invoke --function-name MyLambdaFunction --cli-binary-format raw-in-base64-out --payload '{"what is your name?": "John", "How old are you?": 24}' output.txt
```

