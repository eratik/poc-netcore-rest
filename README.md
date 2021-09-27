# poc-netcore-rest
.Net Core Rest in a Docker Container

This project is a quick POC (control) project to test exposing .Net services via Docker on AWS Fargate.  On Windows this is really straight forward using the AWS Toolkit.  On Mac there are few more steps because everything is done via the AWS CLI.

## Fargate Deployment - Assumptions

- You have a .Net Core Project Running Locally
- You have added Docker Support in the prject (Right-click the project in Solution Explorer and select Add > Docker Support)
- You have Docker Desktop running locally
- You have AWS credentials setup for the target account

## Fargate - Publish Docker Image to ECR - CLI Steps (Mac Only, PC has Publish to AWS option)

- Create your AWS Repo:<br />
`aws ecr create-repository --repository-name oscillo-rest-test --region us-east-1`

- Docker Build your Relase Image:<br />
`docker build -t oscillo-rest-test-2 -f oscillo_rest_test/Dockerfile .`

- Docker Tag your Image<br />
`docker tag oscillo-rest-test-2 {ACCOUNTID}.dkr.ecr.us-east-1.amazonaws.com/oscillo-rest-test`

- Login to the AWS ECR with Docker<br />
`aws ecr get-login-password | docker login --username AWS --password-stdin {ACCOUNTID}.dkr.ecr.us-east-1.amazonaws.com`

- Docker Push your Tagged Image<br />
`docker push {ACCOUNTID}.dkr.ecr.us-east-1.amazonaws.com/oscillo-rest-test`

## Fargate - Configure Cluster - AWS Console OR CLI 

- Create your task definition
- Create your cluster
- Create your service

## Fargate - CI/CD Pipeline
