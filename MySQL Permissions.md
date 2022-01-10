# MySQL Permissions

## Introduction

Hi all,

This is a summary of the privileges that the application and nominal users have on the MySQL bases.

## Prerequisites

Have a database and be an administrator

## Directions

The step by step that we are going to do is the following:

1) NOMINAL MYSQL USERS
2) DBA - TABLE LOWER
3) MYSQL APPLICATION USERS

### Step 1: NOMINAL MYSQL USERS

<img width="646" alt="1" src="https://user-images.githubusercontent.com/81833300/148826224-5f936653-d0b5-4d5e-97f1-94f8a4bedce3.png">

1. UNOs are created together with the scheme or when making a change of ownership.

2. The owner can exclude the desired users from the write time limit.

3. Read, write or admin permissions are managed from dbaccess (https://dbaccess.meliseginf.com/login/?next=/).

### Step 2: DBA - TABLE LOWER

If you need to DROP any of the tables, you must request via Shield to the following flow:

![2](https://user-images.githubusercontent.com/81833300/148826414-9eaf1fad-2510-4c77-9971-2c1a06b61e7d.png)

1. SPECIAL CASES (for example: EXECUTE PROCEDURE, EXECUTE FUNCTION, CREATE TEMPORARY TABLES) contact DBA through Fury support.
2. 
### Step 3: MYSQL APPLICATION USERS

<img width="672" alt="3" src="https://user-images.githubusercontent.com/81833300/148826738-68cff573-dedb-40cf-944d-e7a5dd370238.png">

1. The passwords of the users are sent by email to the owner / creator of the scheme, and from Fury they must be used with the snippets:

<img width="762" alt="4" src="https://user-images.githubusercontent.com/81833300/148826841-da4c269f-acd4-475a-829e-75a31d39eeac.png">

The user * _ADMIN is used from the application to perform batch operations, such as deleting partitions.

If you have any questions or concerns, you can contact us through Fury support :)

Bye











