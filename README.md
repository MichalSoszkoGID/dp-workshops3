## GID DataOps CLI: CI/CD & Quality Control
Welcome to the DataOps CLI Labs workshop repository #3. By the end of this tutorial, you will know how to:
- deploy your code to staging-dev 
- apply dbt tests
- monitor the pipeline's execution with Airflow

Target environment will be Google Cloud Platform's: BigQuery & Data Studio, Vertex AI Managed Notebook, VSCode as IDE. This tutorial was written with GID DataOps 1.0.9 as a current release.

# Excercise

## Commit your project to the remote repository

During previous excercises we've create a local dbt pipeline - which is personal development environment. Now, it is time to review and publish the code so it can be put into staging dev. At this point, our remote repository (the master branch) is empty. Your task is to publish your project by initiating workflow typical for git operations:
- create a new branch
- commit all changes in the code
- publish the branch to the remote repository
- create merge request (or pull request)
- verify if the CI/CD has been executed successfully
- monitor the Airflow for failed jobs
- 
