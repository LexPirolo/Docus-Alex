# Deploy Rollbacked in Booting your app

## Introduction

I tell you that in both Deploy strategies (Blue Green / All-in) in the "Booting your app" step, there is a task that waits for your app to respond to the / ping resource with a status code of 200. This task is retried until 60 times in a 30 second interval on each retry. That is, this task can take up to 30 minutes and then rollback automatically.

## Prerequisites

The basic prerequisites for Troubleshooting is knowing how deployments work in scopes and having access to Fury, Kibana, DataDog, and NewRelic.

## Directions

The step by step that we are going to do is the following:

1) Running locally.
2) Kibana.
3) DataDog / NewRelic 

________

## Step 1): Running locally
The first thing you should do is run your local app with fury run and check that it responds to the resource / ping with 200. There you will be able to see the errors from your console and determine why you cannot deploy in Fury.

If you do not have any error when running fury run, you can use the tools that Fury provides us to perform troubleshooting (Kibana / DataDog / NewRelic) of why the deploy is being rolled back in this case we are going to use Kibana.

## Step 2): Kibana 

I recommend you start with Kibana, here you can see all the logs of your app at the time of deployment. I will leave you some tips to make your search more performant.

<img width="1264" alt="1" src="https://user-images.githubusercontent.com/81833300/142443252-0c671279-fa3a-4a89-9490-6f0f2b4ca0ce.png">

* (1) Here you must indicate the time range of your deploy.
* (2) Here you must add the corresponding filters with your search, you can specify the scope, version, instance, level of the log (error, info, warning), etc.

![2](https://user-images.githubusercontent.com/81833300/142443704-058d32b1-428f-480f-b134-ab3571567482.png)

(choose the tag to filter, example tags.scope)

![3](https://user-images.githubusercontent.com/81833300/142443801-0d1de09b-d601-4ea0-ab6e-3c3dbe328d91.png)

(choose the logical operator)

![4](https://user-images.githubusercontent.com/81833300/142443847-1cd244c7-dff3-4817-ac6d-ae369f45bb7b.png)

(indicate the name of your scope)

*** WARNING! If you are going to use these filters, remove the ones from the query string ***

* (3) Here you can see the logs by version. In case you only want to see the version to deploy, you can add them as a filter. Clicking on (+) it will be added automatically.

![5](https://user-images.githubusercontent.com/81833300/142444110-2094cedd-f8ee-4897-ab2f-c3a9f8b6b957.png)

* (4) Here you can see the logs by instances. In case you only want to see the logs of the new instance (Blue green) you can add them as a filter. Clicking on (+) it will be added automatically.

![6](https://user-images.githubusercontent.com/81833300/142444359-d2b67c4a-6558-46fb-88ea-74e49f4c1446.png)


<img width="1553" alt="7" src="https://user-images.githubusercontent.com/81833300/142445876-683b5b65-b3aa-4faa-ba8a-e5b04496bc37.png">
Finally, in the search bar by query string you can specify words or phrases to search in your logs.
For example:
+ error
-info
err *

## Step 3): DataDog / NewRelic
DataDog & NewRelic, these two tools can be used to see metrics of your app at the time of deployment and understand what happens when the new version is deployed in your app. You can view% CPU, Throughput, Healthy VS Unhealthy Host, Error Rate, Apdex, etc.
This will help you to monitor if your app is being affected by the new version. Remember to make the hourly filters regarding your deploy.







