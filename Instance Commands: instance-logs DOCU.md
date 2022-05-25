# Instance Commands: instance-logs

## Introduction

At the moment in which a deploy is carried out, it remains in the "boot application" step, it does not respond to the /ping resource and the Rollback is generated. No logs are observed demonstrating the failure of the deploy.

<img width="767" alt="1" src="https://user-images.githubusercontent.com/81833300/170336562-efdb6142-cccf-4038-8a37-9c4988761450.png">


## Prerequisites

For that you have to know how to use the terminal tool from the front end of fury and kibana.

## Directions

The step by step that we are going to do is the following:

1) How do i use it?
2) Common errors?

__________

## Step 1): How do i use it?

In order to use this command, it is necessary that at the moment in which the deploy is being carried out we position ourselves on:

Infreaestructure> We select the Scope in which the deployment is being carried out> We select an instance> "Terminal"

![terminal](https://user-images.githubusercontent.com/81833300/136284660-19c3d3a1-49f1-4ead-90c9-38758172b8b9.jpeg)

* Inside the terminal we will execute any command at ease:

>1. By Default: instance-logs (shows only the amount of 10 lines)
>2. Per line: instance-logs --lines = 100 (number of lines to be displayed by the user, in this case we give the example of 100)
>3. By Keep tailing: instance-logs -f

#### ***Warning:***

 * Execute the command at the moment in which the deployment is being carried out, if possible in boot your app.
* In case you are deploying with Bluegreen or Canary strategy, check that the selected instance belongs to the Candidate.
______________

## Step 2): ***Common errors?***

* In most cases, the error comes from the application side, that is, it is not an issue with the Fury infrastructure.

Some tips to check:

- First of all it is necessary to know if the version runs well locally with fury run.

- Look at the deploy Kibana, it can show the exact error and help identify the problem.

<img width="1495" alt="Captura de Tela 2022-05-25 às 15 12 14" src="https://user-images.githubusercontent.com/81833300/170338263-36a7867a-c2cf-4e48-8d8a-152b9e14d87f.png">

Path of the application in dockerfile, check if it has the correct name and if everything is correct:

![from](https://user-images.githubusercontent.com/81833300/136287640-62ad33d2-64be-481f-8add-e73d131efc79.png)

Especially if the error is / ping, check if it consumes secrets, connections to other services (db, kvs, bq, etc), and if the names are correct according to the service snippets on the fury page.
