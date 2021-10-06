# Instance Commands: instance-logs

#### ***Issues:***

``` At the moment in which a deploy is carried out, it remains in the "boot application" step, it does not respond to the /ping resource and the Rollback is generated. No logs are observed demonstrating the failure of the deploy.```

![steps deploy](https://user-images.githubusercontent.com/81833300/136280680-d4cb4bb8-5f24-407c-a2bd-ab368f34c339.jpeg)

#### ***Workaround:***

```At present, we provide an instance command so that the logs of the deploy process can be obtained, which help us to understand the reason why the deploy is not being able to be performed.```
 
```The available command is: "instance-logs" ```
 
```What this command does is execute a tail, showing the last lines, by default it will print the last ten lines of its input data to the standard output. In turn, we can discriminate by number of lines or by keep tailing.```
__________

### ***How do i use it?***

* In order to use this command, it is necessary that at the moment in which the deploy is being carried out we position ourselves on:

  >Infreaestructure> We select the Scope in which the deployment is being carried out> We select an instance> "Terminal"

![terminal](https://user-images.githubusercontent.com/81833300/136284660-19c3d3a1-49f1-4ead-90c9-38758172b8b9.jpeg)

* Inside the terminal we will execute any command at ease:

>1. By Default: instance-logs (shows only the amount of 10 lines)
>2. Per line: instance-logs --lines = 100 (number of lines to be displayed by the user, in this case we give the example of 100)
>3. By Keep tailing: instance-logs -f

#### ***Warning:***

> - Execute the command at the moment in which the deployment is being carried out, if possible in boot your app.

> - In case you are deploying with Bluegreen or Canary strategy, check that the selected instance belongs to the Candidate.
______________

### ***What are the common errors?***

* In most cases, the error comes from the application side, that is, it is not an issue with the Fury infrastructure.

```Some tips to check:```

> - First of all it is necessary to know if the version runs well locally with fury run.

> - Look at the deploy Kibana, it can show the exact error and help identify the problem.

![kibana](https://user-images.githubusercontent.com/81833300/136287493-46763ac3-2176-42b9-b95e-14b64012e42d.png)

> - Path of the application in dockerfile, check if it has the correct name and if everything is correct:

![from](https://user-images.githubusercontent.com/81833300/136287640-62ad33d2-64be-481f-8add-e73d131efc79.png)

> - Especially if the error is / ping, check if it consumes secrets, connections to other services (db, kvs, bq, etc), and if the names are correct according to the service snippets on the fury page.
