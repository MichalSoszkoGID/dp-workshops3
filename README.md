## GID DataOps CLI: CI/CD & Quality Control
Welcome to the DataOps CLI Labs workshop repository #3. By the end of this tutorial, you will know how to:
- deploy your code to staging-dev 
- apply dbt tests to your project
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

For that you can follow step-by-step instruction presented below:
**Step 1.** 
Inside your JupyterLab notebook launch VSCode and navigate to your project. Create new local branch by clicking on the Git icon on lower-left side of the screen:

<img src="https://user-images.githubusercontent.com/97670480/192233080-d03f3863-0f3c-4be8-a75e-e0a0c196072f.png"  width="40%" height="40%">

and typing new branch name (this step executes the `git branch checkout` CLI command equivalent for VSCode):

<img src="https://user-images.githubusercontent.com/97670480/192233893-4d7ce5d0-30d9-4618-868f-025585f255e2.png"  width="40%" height="40%">

**Step 2.**
Open Source Control tab by either pressing `Shift+CTRL+G` or clicking on the icon:

<img src="https://user-images.githubusercontent.com/97670480/192230701-ea2679fa-b064-42f0-8e8b-0cc08694fbd3.png"  width="30%" height="30%">

---
**Step 3.**
In the Source Control Tab put your changes to the code to staging phase (at this point the whole project's code is new) by clicking on "Stage All Changes" icon:

<img src="https://user-images.githubusercontent.com/97670480/192231747-6bbc5c97-2273-4735-8e6a-9b80e12419cc.png"  width="30%" height="30%">

...paste commit message, ie: `Populate branch with dp project` and click on `Commit` icon:

<img src="https://user-images.githubusercontent.com/97670480/192234948-629fc805-c4fd-47cf-9cf5-894c6934921b.png"  width="30%" height="30%">

---
**Step 4.**
Publish the branch and provide your GitLab credentials:

<img src="https://user-images.githubusercontent.com/97670480/192236772-39d4dcd1-02c7-4b25-a0d3-bc9e43eb5663.png"  width="70%" height="70%">

>-> Hint: If you use Git for the first time in your workbench you will have to set global git variables for your identification, for that, type the following lines of code in the VSCode / notebooks terminal:
```
git config --global user.email "John.Doe@example.com"
git config --global user.name "John Doe"
```

---
**Step 5.** Navigate to repository folder: https://gitlab.com/datamass-mdp-workshop and select your project. Then locate its branch list and click on your newly published branch:

<img src="https://user-images.githubusercontent.com/97670480/192237880-f52504e5-255d-433a-8ac7-9d13e63f9203.png"  width="25%" height="25%">
---

...and wait until the CI/CD phase finishes the job:

<img src="https://user-images.githubusercontent.com/97670480/192238482-59abc646-1b0f-469d-b0d6-ee02d6c1e100.png"  width="60%" height="60%">
---

**Step 6.**
Having the CI/CD succesfully completed means the DAG has been created without failures and it has been sent to the composer. In order to track your project DAG in Airflow enter the following link: https://58a6f530618c49558667b865f21ac64a-dot-europe-central2.composer.googleusercontent.com/home and locate your project.

>-> Hint: It can take few minutes between succesfull CI/CD fun and Airflow DAG import. Do not worry, it is going to be there in not time!

In DAGs folder click on your project and manualy trigger the run (the DAG schedule time has been set up during project initialization, the default value for most project is `0 12 * * *`)

<img src="https://user-images.githubusercontent.com/97670480/192253627-b3be7169-44c1-43d0-bff1-a0c93f90f6c4.png"  width="60%" height="60%">
