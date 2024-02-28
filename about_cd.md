# Deploy Django on EC2 - GitHub Actions Workflow

## Overview

This GitHub Actions workflow automates the deployment of a Django application on an EC2 instance. It is triggered on pushes to the `release` branch and can also be manually triggered using the GitHub Actions interface.

## Workflow Steps

1. **Checkout Repository**: This step checks out the repository to make the workflow aware of the latest changes.

2. **Convert SSH Private Key to PEM**: The SSH private key stored in the GitHub repository secrets is converted to the PEM format required for SSH authentication.

3. **Set up SSH**: This step sets up SSH authentication using the converted private key. It utilizes the `webfactory/ssh-agent` action to securely handle SSH authentication.

4. **Add EC2 IP to Known Hosts**: The public IP address of the EC2 instance is added to the known hosts file to establish a secure SSH connection without manual intervention.

5. **SSH into EC2 Instance**: This step establishes an SSH connection to the EC2 instance using the configured private key. It then performs the following tasks:
    - Enters the project directory on the EC2 instance.
    - Pulls the latest changes from the `release` branch of the repository.
    - Stops and removes existing Docker containers.
    - Builds and starts Docker containers for the Django application.

## Secrets

This workflow relies on the following GitHub repository secrets:
- `SSH_PRIVATE_KEY`: The SSH private key used for authentication with the EC2 instance.
- `EC2_PUBLIC_IP`: The public IP address of the EC2 instance.

Ensure that these secrets are securely stored in the GitHub repository settings.

## Trigger

The workflow is triggered under the following conditions:
- Pushes to the `release` branch.
- Manual triggering through the GitHub Actions interface.

## Prerequisites

Before using this workflow, ensure the following prerequisites are met:
- An EC2 instance is set up and accessible via SSH.
- Docker is installed on the EC2 instance.
- The Django application is configured for Docker deployment.

## Usage

To use this workflow:
1. Configure the required secrets in the GitHub repository settings.
2. Create a `release` branch and push your changes to trigger the workflow.
3. Monitor the workflow execution for any errors or failures.
4. Access the deployed Django application on the EC2 instance.
****