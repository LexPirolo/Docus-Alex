# Inactive scopes basics. Why are they inactivated? What happens to the scope when this happens?

  #### When a scope is marked as inactive, its infrastructure (instances, load balancer, etc.) is completely erased, but all settings related to it are kept. In this way, the scope remains registered in the app with the configuration it had before being inactivated.


* ***Why will my scopes be inactivated?***

  This is because the scope in question is not "Productive" (it does not have alerts set), it is not associated with an Nginx rule, and it had no activity in the last 2 days, that is, it had no deployments or changes in the configuration in the indicated time.

* ***How can I re-activate it?***

  You can do it from the front-end of Fury in the section: Scopes> Filter the
search by scope name> Click Activate. This will generate an Initial deploy and you will be able to select the version to deploy.

* ***My scope is productive, why is it being inactivated?***

  Yes, your scope is productive, it must have the corresponding alerts configured. This way the scope will not be inactivated.


#### Any questions or queries do not hesitate to contact us through the Fury Support Chat

* ##### In case you receive an email indicating that your scope (productive) will be inactivated, check if it has the corresponding fins configured.
____


    To reactivate an inactive scope, enter the Scopes section from the Fury front-end, and click on the "Activate" button. 
    This will generate an Initial type deploy (since you are creating the infrastructure again), and will allow the 
    deployment of new versions.
  ![reactivar](https://user-images.githubusercontent.com/81833300/136220712-8239129e-71b3-4e5b-aafb-2f29a93b4366.png)
  
    If you want to prevent your scope from being marked as inactive after receiving the notification, you will have the 
    "Extend" button, which will allow your scope to continue active for a further 48 hours.
![Extend](https://user-images.githubusercontent.com/81833300/136220962-9a02aed4-0917-4f78-82d3-2bf6e1dfed6f.png)