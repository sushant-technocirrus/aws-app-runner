# Deployment Workflows

This repository contains two deployment workflows: `deploy-dev.yml` and `deploy-test.yml`. These workflows are designed to deploy an application to the Amazon App Runner service in different environments: "dev" and "test".

## Prerequisites

Before using these workflows, make sure you have the following prerequisites in place:

- An AWS account with appropriate permissions to deploy resources using Amazon App Runner.
- Docker installed on the machine where the workflows will be executed.
- AWS credentials (access key and secret access key) with sufficient permissions to access the necessary AWS resources.
- An existing Amazon Elastic Container Registry (ECR) repository to push the Docker image for deployment.
- An AWS IAM role ARN with sufficient permissions to deploy resources using Amazon App Runner.

## Workflow Files

The repository contains the following workflow files:

1. `deploy-dev.yml`: This workflow deploys the application to the "dev" environment.
2. `deploy-test.yml`: This workflow deploys the application to the "test" environment.

## Usage

To use these workflows, follow the steps below:

1. **Fork** this repository to your own GitHub account or **clone** it to your local machine.

2. Open the desired workflow file (`deploy-dev.yml` for the dev environment or `deploy-test.yml` for the test environment) and update the following placeholders with your own values:

   - `service`: The name of your App Runner service.
   - `aws-access-key-id`: The AWS access key ID secret stored in your GitHub repository secrets.
   - `aws-secret-access-key`: The AWS secret access key secret stored in your GitHub repository secrets.
   - `aws-region`: The desired AWS region for the respective environment (e.g., "us-west-2" for the dev environment).
   - `access-role-arn`: The ARN of the AWS IAM role with sufficient permissions to deploy resources using Amazon App Runner.

3. **Commit** the changes and **push** them to your GitHub repository.

4. Open the GitHub repository page in your browser and navigate to the **"Actions"** tab.

5. Select the desired workflow ("Deploy to App Runner - Dev Environment" or "Deploy to App Runner - Test Environment") and click on the **"Run workflow"** button.

6. In the workflow run page, provide the required input values, such as the environment (e.g., "dev" or "test").

7. Start the workflow run by clicking the **"Run workflow"** button.

8. The workflow will execute the necessary steps to build and deploy the application to the specified environment using Amazon App Runner.

## Workflow Steps

Each deployment workflow consists of the following steps:

1. **Checkout**: Checks out the repository code.

2. **Configure AWS credentials**: Configures the AWS credentials using the provided access key and secret access key.

3. **Login to Amazon ECR**: Logs in to the Amazon Elastic Container Registry (ECR) to authenticate Docker for pushing the image.

4. **Build, tag, and push image to Amazon ECR**: Builds the Docker image, tags it with the commit SHA, and pushes it to the specified ECR repository.

5. **Deploy to App Runner**: Deploys the application to the App Runner service in the specified environment, using the image built in the previous step.

   - For the dev environment, the workflow uses the `awslabs/amazon-app-runner-deploy@main` action.

   - For the test environment, the workflow uses the `awslabs/amazon-app-runner-deploy@main` action with additional configuration for the desired region and stability wait duration.

## Monitoring the Deployment

Once the deployment workflow is triggered, you can monitor its progress in the GitHub Actions workflow run page. The workflow will provide detailed logs for each step and indicate whether the deployment was successful or encountered any errors.

You can also monitor the deployed application's status in the Amazon App Runner console or use AWS CLI commands to get more information about the deployed service.

## Cleanup

Remember to clean up any unused resources to avoid unnecessary costs. You can delete the App Runner service, ECR repository, and any associated resources when they are no longer needed.

## Conclusion

These deployment workflows provide a convenient way to deploy an application to Amazon App Runner in different environments. By following the provided instructions, you can easily configure and use these workflows to automate your deployment process.
