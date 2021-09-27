# poc-netcore-rest
.Net Core Rest in a Docker Container

This project is a quick POC (control) project to test exposing .Net services via Docker on AWS Fargate.  On Windows this is really straight forward using the AWS Toolkit.  On Mac there are few more steps because everything is done via the AWS CLI.

## Fargate Deployment - Assumptions

-- You have a .Net Core Project Running Locally
-- You have added Docker Support in the prject (Right-click the project in Solution Explorer and select Add > Docker Support)
-- You have Docker Desktop running locally
-- You have AWS credentials setup for the target account

## Fargate Setup - Steps

-- Create your AWS Repo:
`aws ecr create-repository --repository-name oscillo-rest-test --region us-east-1`

-- Docker Build your Relase Image:
`docker build -t oscillo-rest-test-2 -f oscillo_rest_test/Dockerfile .`

-- Docker Tag your Image
`docker tag oscillo-rest-test-2 818038840593.dkr.ecr.us-east-1.amazonaws.com/oscillo-rest-test`

-- Login to the AWS ECR with Docker
`aws ecr get-login-password | docker login --username AWS --password-stdin 818038840593.dkr.ecr.us-east-1.amazonaws.com`

-- Docker Push your Tagged Image --
docker push 818038840593.dkr.ecr.us-east-1.amazonaws.com/oscillo-rest-test


