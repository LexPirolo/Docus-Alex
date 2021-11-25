# Golden Gate as a Service | MySQL

## Introduction

Hi,

This is a tutorial to set up a BigQ topic with the latest news from your database. This new method replaces the java-workers used by Golden Gate.

## Prerequisites

Mysql 5.7 and above, have your database created and have knowledge of BigQ.

## Improvements

What transaction types will the topic receive?
* Inserts: PK column
* Updates: PK column + updated columns
* Deletes: PK column

Adding new fields
* You can add new fields dynamically to your topics and they will be available within seconds.

Monitoring your BigQ Topics:
* On the left panel, go to > BigTopics option. Select your topic in the monitor section.
____________

## Important notice:

Due to a known limitation in GoldenGate for MySQL, it is not supported to ALTER replicated tables WITHOUT stopping GoldenGate's replication process before.

Please contact DBA Team @ Fury support before executing a Migration in a table being replicated to BigQ with GoldenGate to arrange to stop the replication before and resuming it after the migration completes.
_____

## How to use GGaaS for MySQL

1. Log in to Fury and then find your app.
2. On the left panel, go to Database.
3. Select your database and then click the "Send news to BigQ" button.

<img width="239" alt="1" src="https://user-images.githubusercontent.com/81833300/143494895-a352f1e8-1d15-432e-a75d-2f68ea7c6a38.png">

4. Select the tables and columns (PK only) you want to extract.

<img width="1440" alt="2" src="https://user-images.githubusercontent.com/81833300/143494949-8af94485-cb4c-47fd-bcb3-15bb514bf5de.png">

5. Press OK.

```Addendum#```
```The creation process takes a few minutes, once it finishes the topic will be ready.```

6. Go to the left panel , and select BigQ Topics.
7. Your new topic will be displayed with the following format: mysql-simple-db_name-table_name.dbaasapirest ( .dbaasapirest is mandatory )

```Finally, you can create a consumer for this topic :)```

<img width="1440" alt="3" src="https://user-images.githubusercontent.com/81833300/143495048-9fab46d3-f897-4bd0-851d-2e015623e046.png">

8. You must create a consumer to receive news.

## NOTES:

* This solution does not guarantee to maintain the order of news and also you may also receive duplicated items.
* You can only add PK columns.
* The MyISAM storage type tables are not supported for GoldenGate.
* You cannot select tables that have columns of these data types: xml, set, json, spatial types (geometry, point, linear chain, polygon, multipoint, multiline, multipolygon, geometry collection)
* Neither you can add a column of those types after topic creation. This will BREAK the topic.
* This feature is not available for test databases (those hosted on any of the test clusters) (e.g: desaenv00, desaenv01, etc).
* You cannot delete a field once it is added to your topic.





