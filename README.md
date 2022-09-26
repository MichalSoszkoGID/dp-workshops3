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

## Deploy your project to stage-dev and monitor pipeline in Airflow

Having the CI/CD succesfully completed means the DAG has been created without failures and it has been automaticaly sent to the composer. In order to track your project DAG in Airflow enter the following link: https://58a6f530618c49558667b865f21ac64a-dot-europe-central2.composer.googleusercontent.com/home and locate your project.

>-> Hint: It can take few minutes between succesfull CI/CD fun and Airflow DAG import. Do not worry, it is going to be there in not time!

In DAGs folder click on your project and manualy trigger the run (the DAG schedule time has been set up during project initialization, the default value for most project is `0 12 * * *`)

<img src="https://user-images.githubusercontent.com/97670480/192253627-b3be7169-44c1-43d0-bff1-a0c93f90f6c4.png"  width="60%" height="60%">

Now, you can monitor execution of your pipeline. With the project of our size it should take ca. 10 minutes.

## Add dbt tests to your project

Tests are utterly important part of any data pipeline. In theory, if the code is right, data should be also correct. However, even for easy pipelines, subsequent and continuous code modification, adding new sources, changes in business logic etc. greatly increases risk of duplication, nullification, incorrect aggregations, and as result - greatly affects the analytics (in a negatie way). In this excercise you will add three types of tests to your local development instance of dbt and then transfer them into Airflow. 

Your task is to add:

- at least 1 core generic dbt test from the list: [`unique`, `not_null`, `accepted_values`, `relationships`]

>-> Hint: You can test whatever dbt resource (model, seed, snapshot) you want, keep in mind, that the utlimate goal is to serve data mart models of highest quality. Thus apart from engineering tests like not_null, unique it is good to apply more business related checks as well.

- at least 1 package-offered generic dbt test using one of the following dbt packages: dbt_expectations, dbt_utils

>-> Hint: Tests offered by external packages are more soffisticated and offer greater usability. If you know your data well, you will also know what kind of records it is not supposed to return and what kind of logic relations (or statistic divergence) is not allowed.

- at least 1 custom (singular) test.

>-> Hint: Finally, if you haven't found the generic tests that answer your needs, you can create the test of your own. This is especially helpfull when you want to design a business-oriented data quality check. Ie, if you are sure your timeseries data cannot follow a specific trend (let's say - it is nearly impossible to recieve 90 % loss in revenue for a specific period of time), then you can create an assertion in dbt that monitors that. Just remember - test fails whenever there are any records returned by the test query, so if your tests is about counting records... it will always fail!

>-> Hint: After you configure your `yml` files to contain recipes for tests don't forget to execute the `dbt test` command and check whether they run as as intended. 

After you've implemented the tests on your local dbt instance you will need to deploy your code to the remote repository and trigger the CI/CD + Airflow pipelines. 
We encourage you to try this task on your own. However, if you'd like to follow our solution example, please continue to the next chapter!

### Bonus Excercise ###

If your pipeline finishes run on staging-dev with "all green" try and play around with tests, making them to fail badly! For that you can brak your models, modify tests logic (esp. for singular tests), narrow test boundary conditions etc.

### Adding tests - examples

In this chapter we'd like to provide couple of examples on how to implement tests descrubed in the exercise. Note that we will use here the models created during Session 2 Excercises. If you need to catch-up please refer to the following repository: <link>. This repository stores the complete dbt project example created so far durinf Session 2 demonstration and hands-on excercises, feel free to copy-paste models into your local instance of dbt if you need.

