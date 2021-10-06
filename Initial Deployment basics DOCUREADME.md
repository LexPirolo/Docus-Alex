# Initial Deployment basics. What does? What do I do if it is in status: error?

#### The Initial Deployment is the first deploy that all scope receives after its creation or activation. This is where the scope infrastructure is created, it is validated that the instances respond to the LB and that the application responds to the / ping resource with status 200.
![deploy](https://user-images.githubusercontent.com/81833300/136229321-436b529b-89df-4f05-8f0b-1bec3009d486.png)

#### If the version to deploy does not work, that is, it does not respond to /ping, the deploy fails. This is why the scope status is in "error"
  ![scope error](https://user-images.githubusercontent.com/81833300/136229575-a7d054ce-c89c-48e9-98f0-aa09fc8d851b.png)



***To avoid this problem, the best practice is to always deploy a basic version for the first time, which responds to the / ping resource with status 200, without anything else. In this way, after the initial deployment has finished correctly, you will be able to deploy your more advanced versions and with more features, ensuring a correct deployment and avoiding the error status.***

***Now, if our initial is in error, there is no more to do than delete the scope and recreate it. It must be borne in mind that if the scope that was in error is productive, before deleting it, we must eliminate the Alerts that it has configured, otherwise we will not be able to do it.***
