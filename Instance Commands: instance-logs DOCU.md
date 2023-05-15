# Logs and Instance Commands: instance-logs

## Introduction

At the moment in which a deploy is carried out, it remains in the "boot application" step, it does not respond to the /ping resource and the Rollback is generated. No logs are observed demonstrating the failure of the deploy.

<img width="767" alt="1" src="https://user-images.githubusercontent.com/81833300/170336562-efdb6142-cccf-4038-8a37-9c4988761450.png">


## Prerequisites

For that you have to know how to use the terminal tool from the front end of fury, kibana and granafa.

## Directions

The step by step that we are going to do is the following:

1) Common errors? 
    - Fury Run
    - Kibana
    - Grafana
    -  Dockerfile
    
2) Terminal, How do i use it?

__________

## Step 1): ***Common errors?***

* In most cases, the error comes from the application side, that is, it is not an issue with the Fury infrastructure.

Some tips to check:

1) First of all it is necessary to know if the version runs well locally with fury run.

2) Look at the deploy Kibana, it can show the exact error and help identify the problem.

<img width="1429" alt="1" src="https://github.com/LexPirolo/Docus-Alex/assets/81833300/1160407d-5a39-4a8f-9875-f66317a7ca8d">

Clicking on Kibana loads the screen with all the logs, what we can do here is put the error search field and filter the deploy date

<img width="1723" alt="5" src="https://github.com/LexPirolo/Docus-Alex/assets/81833300/79de4a2b-99af-4a3d-a84f-a7126caf5712">

Below in message we already see the error with the filter

<img width="1727" alt="image" src="https://github.com/LexPirolo/Docus-Alex/assets/81833300/89b9e485-ac8a-4216-9e2f-80e6ed900707">


3) It is also possible to check the Grafana dashboard to see if there are any errors.
 
To access the Grafana dashboard we need the Deployment ID, it is the numeral that is contained in the deploy link

<img width="1791" alt="0 1" src="https://github.com/LexPirolo/Docus-Alex/assets/81833300/195ae434-d9c7-49d1-be07-36d29f9f1332">

In Grafana we put the deployment ID that we got in fury in the Deployment field, when loading the information we have some dashboards with logs regarding the containers, the number of errors, etc.

<img width="1717" alt="2" src="https://github.com/LexPirolo/Docus-Alex/assets/81833300/4cfd735c-f036-478e-bdba-7de060159289">

To verify the errors we go down in the dashboard Error/ Severe/ Panic logs. Here the word error is marked in yellow

<img width="1726" alt="3" src="https://github.com/LexPirolo/Docus-Alex/assets/81833300/d69f84de-09b8-407b-9f13-5f8444f4c7d6">


4) Path of the application in dockerfile, check if it has the correct name and if everything is correct:

![from](https://user-images.githubusercontent.com/81833300/136287640-62ad33d2-64be-481f-8add-e73d131efc79.png)

______________

## Step 2): Terminal, How do i use it?

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
  * Remembering that to see logs through the terminal is only possible for Standart scopes, it is not possible to see from severless scopes.

Especially if the error is / ping, check if it consumes secrets, connections to other services (db, kvs, bq, etc), and if the names are correct according to the service snippets on the fury page.
