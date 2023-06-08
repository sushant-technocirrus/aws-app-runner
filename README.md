# Deploy to App Runner - Image based

![Image Based](https://github.com/sushant-technocirrus/aws-app-runner/assets/122975959/89c6b16c-5620-4cc5-a819-5e182fee2e95)


This GitHub Actions workflow simplifies the deployment of your application to AWS App Runner using Docker images. Automate your deployment process and effortlessly deploy your application to different environments (Dev, Test, Prod) with ease.

## Workflow Triggers

The workflow can be triggered in two ways:

- **Push Event**: Whenever there is a push to the `main` branch, the workflow is automatically triggered.
- **Manual Execution**: You can manually trigger the workflow by selecting the desired environment from the provided options.

## Deployment Environments

The workflow supports deployment to three robust environments: Dev, Test, and Prod. Choose the environment that best suits your needs when triggering the workflow manually.

### Dev Environment

The Dev environment is designed for rapid development and testing. It deploys the application to the `us-west-2` region, ensuring a seamless testing experience. Once the deployment is complete, the workflow will display the App Runner service ID for the Dev environment.

### Test Environment

The Test environment is perfect for comprehensive testing and quality assurance. It deploys the application to the `us-east-1` region, providing a controlled environment for thorough testing. After the deployment finishes, the workflow will reveal the App Runner service ID for the Test environment.

### Prod Environment

The Prod environment is the ultimate destination for your application. It deploys the application to the `us-east-2` region, offering a highly available and scalable production environment. Once the deployment is complete, the workflow will unveil the App Runner service ID for the Prod environment.

## Prerequisites

Before using this workflow, ensure you have completed the following steps:

1. **AWS Credentials**: Set up your AWS credentials by adding the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` secrets to your GitHub repository.
2. **IAM Role**: Create an AWS IAM role with the necessary permissions and store the ARN of the role as the `ROLE_ARN` secret in your repository.

## Customizing the Workflow

You have the flexibility to customize the workflow by modifying the following parameters:

- `ECR_REPOSITORY`: Update the name of the ECR repository where the Docker image will be pushed.
- `region`: Adjust the desired region for each environment's deployment.

For further details on customizing the workflow and exploring advanced usage, refer to the [official GitHub Actions documentation](https://docs.github.com/en/actions).

## Workflow Outputs

After each successful deployment, the workflow provides the following outputs:

- **Dev Environment**: The App Runner service ID for the Dev environment.
- **Test Environment**: The App Runner service ID for the Test environment.
- **Prod Environment**: The App Runner service ID for the Prod environment.

#
