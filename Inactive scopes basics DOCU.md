# Inactive scopes basics. Why are they inactivated? What happens to the scope when this happens?

## Introduction

When a scope is marked as inactive, its infrastructure (instances, load balancer, etc.) is completely erased, but all settings related to it are kept. In this way, the scope remains registered in the app with the configuration it had before being inactivated.

## Prerequisites

For this it is necessary to understand how to check the status of the scope and how to reactivate that scope.

## Directions

The step by step that we are going to do is the following:

1) To reactivate an inactive scope.

### Step 1: To reactivate an inactive scope.
To reactivate an inactive scope, enter the Scopes section from the Fury front-end, and click on the "Activate" button. This will generate an Initial type deploy (since you are creating the infrastructure again), and will allow the deployment of new versions.

    
<img width="1523" alt="scope inactivo" src="https://user-images.githubusercontent.com/81833300/172380308-bf01a4a1-0bc3-49de-8324-65df1c4e37cb.png">

<img width="1516" alt="activate" src="https://user-images.githubusercontent.com/81833300/172380385-271c2000-f5eb-4051-8fc2-7045e47c4fa0.png">

<img width="1082" alt="escolher a versão" src="https://user-images.githubusercontent.com/81833300/172380466-3dbe350c-7e5a-417c-acde-0eee5f6f4493.png">



## Questions
1) Why will my scopes be inactivated?
2) How can I re-activate it?
3) My scope is productive, why is it being inactivated?


1)Why will my scopes be inactivated?

    This is because the scope in question is not "Productive" (it does not have alerts 
    set), it is not associated with an Nginx rule, and it had no activity in the last 
    2 days, that is, it had no deployments or changes in the configuration in the 
    indicated time.

2)How can I re-activate it?

    You can do it from the front-end of Fury in the section: Scopes> Filter the search 
    by scope name> Click Activate. This will generate an Initial deploy and you will be 
    able to select the version to deploy.

 
3)My scope is productive, why is it being inactivated?***

    Yes, your scope is productive, it must have the corresponding alerts configured. 
    This way the scope will not be inactivated.


* ***If you receive an email informing you that your (productive) scope will be inactivated, check if it has the corresponding alerts configured.***


#### Any questions or queries do not hesitate to contact us through the Fury Support Chat
