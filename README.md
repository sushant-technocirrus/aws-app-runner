# Deploy to App Runner - Image based

![Image Based](https://github.com/sushant-technocirrus/aws-app-runner/assets/122975959/9e42f9cc-0a86-4074-b2ea-b47fc1a87334)

## Workflow Overview

Welcome to the Deploy to App Runner workflow! This GitHub Actions workflow automates the seamless deployment of your Docker image to AWS App Runner, saving you time and effort. Whether you're pushing updates to the `main` branch or manually triggering the workflow, it ensures a smooth deployment process.

## Workflow Triggers

The workflow is triggered in two scenarios:

1. **Push to `main` Branch**: Whenever a new commit is pushed to the `main` branch, the workflow is automatically triggered.

2. **Manual Invocation**: The workflow can also be manually invoked by selecting the "Run workflow" option in the Actions tab of the repository.

## Workflow Steps

1. **Checkout**:
   - This step checks out the repository code to access the necessary files for building and deploying the Docker image.

2. **Configure AWS credentials**:
   - In this step, AWS credentials are configured using the provided secrets. The workflow uses the `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, and `AWS_REGION` secrets to authenticate and authorize AWS API calls.

3. **Login to Amazon ECR**:
   - This step logs in to Amazon Elastic Container Registry (ECR) using the AWS credentials configured in the previous step. It authenticates Docker to interact with the ECR repository.

4. **Build, tag, and push image to Amazon ECR**:
   - In this step, a Docker image is built, tagged with a unique identifier (using the commit SHA), and pushed to the specified Amazon ECR repository. The built image is based on the repository's code and any specified Dockerfile.

5. **Deploy to App Runner**:
   - This step deploys the Docker image to AWS App Runner. It uses the AWS App Runner service to create and manage the deployment. The `service` parameter specifies the name of the service, and the `image` parameter references the Docker image pushed to Amazon ECR in the previous step. Additionally, the `access-role-arn` secret provides the ARN of the IAM role with the necessary permissions for the deployment. The `region` secret specifies the AWS region in which the deployment will occur. The `wait-for-service-stability` parameter ensures that the workflow waits until the service reaches a stable state before proceeding.

6. **App Runner output**:
   - Finally, this step displays the output of the App Runner deployment. It echoes the service ID of the deployed App Runner service, which can be useful for further processing or monitoring.

## Secrets Used

The workflow utilizes the following secrets from the repository's settings:
- `AWS_ACCESS_KEY_ID`: AWS access key ID.
- `AWS_SECRET_ACCESS_KEY`: AWS secret access key.
- `AWS_REGION`: AWS region.
- `ROLE_ARN`: Access role ARN.

> Note: Make sure to set up the required secrets in your GitHub repository's settings before using this workflow.
