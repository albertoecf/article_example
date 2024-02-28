# Django CI - GitHub Actions Workflow

## Overview

This GitHub Actions workflow automates the continuous integration (CI) process for a Django application. It runs tests on pull requests targeting the `main` branch and can also be manually triggered using the GitHub Actions interface.

## Workflow Steps

1. **Set up PostgreSQL Service**: This step sets up a PostgreSQL service container for running tests. It initializes a PostgreSQL database with predefined credentials and exposes it on port 5432.

2. **Checkout Code**: The workflow checks out the repository to make the CI process aware of the latest code changes.

3. **Set up Python**: This step sets up the Python environment required for running Django tests. It specifies the Python version to use.

4. **Install pipenv**: Pipenv, a package manager for Python, is installed to manage dependencies.

5. **Install Dependencies with pipenv**: The workflow installs project dependencies using pipenv. It navigates to the backend directory and installs both regular and development dependencies.

6. **Create .env file**: This step creates a `.env` file containing environment variables required for running the Django application and tests. It includes sensitive information such as database credentials and API keys.

7. **Run Django Tests**: Finally, the workflow executes Django tests using the `python manage.py test` command within the backend directory.

## Secrets

This workflow relies on the following GitHub repository secrets:
- `SECRET_KEY`: Secret key used for Django application encryption.
- `AWS_ACCESS_KEY_ID`: AWS access key ID for AWS services integration.
- `ADD_KEYS_HERE`

Ensure that these secrets are securely stored in the GitHub repository settings.

## Trigger

The workflow is triggered under the following conditions:
- Pull requests targeting the `main` branch.
- Manual triggering through the GitHub Actions interface.

## Prerequisites

Before using this workflow, ensure the following prerequisites are met:
- PostgreSQL service is accessible on port 5432.
- Python and pipenv are installed on the CI environment.
- Django application is configured for testing with a PostgreSQL database.

## Usage

To use this workflow:
1. Configure the required secrets in the GitHub repository settings.
2. Create pull requests targeting the `main` branch and monitor the workflow execution for any errors or failures.
3. Ensure all tests pass before merging pull requests into the `main` branch.
