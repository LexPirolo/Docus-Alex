# Partition a table in MySQL

## Introduction

Hello everyone,

From DBA we want to share this information related to partitions in MySQL.

The big question we need to ask is For serving us?
It is a way to optimize the performance of the database and helps us to:

* Separate the information from our tables into different partitions, thus achieving faster queries.
* Reclaim disk space by quickly deleting records without having to loop through the entire table.
* It is transparent for the application, that is to say that the code does not have to be adapted to know in which partition the registers are.

## Prerequisites

Have a database and be an administrator

## Partition types

By rank:
We can build our partitions by specifying a range of values ​​defined on a certain column of the table. (This type of partition is the one that is commonly used).

By lists:
We can build our partitions by specifying a list of concrete values. That is, we will indicate the number of partitions to create, and for each partition, the list of values ​​that will be the condition to insert in it.

By hashes:
MySQL takes care of distributing the logs automatically using a modulus operation. You just have to pass it a column or expression that results in an integer (the hash) and the number of partitions you want to create.

By key:
Similar to hash partitioning, but in this case we don't need to pass an integer. MySQL will use its own hash function to generate it. (If no column is specified to generate the hash from, the default primary key is used.)

By composition:
We can combine the different partitioning methods and create partitions of partitions.

## Directions

1) How to partition my table
2) Syntax
3) To consider
4) Procedure to add partitions

### Step 1: How to partition my table?
You can use these two ways to partition the current table:

#### Scenario 1: 
```(It is the one we recommend from DBA)```

- Create a new table (B) with the same structure as the original table + the corresponding partitions.
> In case it is required to keep some records in the new table, eg: last month: Insert the records from the original table (A) to the new table (B). (If there are several records, use a cursor) .
- Rename the original table (A) to history. (This process is instant).
- Rename the new table (B) to the original. (This process is instant).
-  New records are inserted into table (B) while table (A) can be left as history or deleted.

#### Scenario 2:
Make the altar to the current table with the corresponding partitions. (Depending on the size of the table and the traffic, it could generate performance problems in the db).

### Step 2: Syntax

How do we create a partitioned table?
In the following example we show the syntax for creating a table partitioned by month:

create table `test` (`id` varchar(10) not null, `user_id` bigint(5), `created` datetime not null, primary key (`id`, `created`)) partition by range (extract(year_month from `created`)) ( partition old values ​​less than (201810), partition p1 values ​​less than (201811), partition p2 values ​​less than (201812), partition pdefault values ​​less than maxvalue );

** The pdefault partition will have all the records that do not fit in the created partitions. (In this way we make sure that the information will never stop being inserted in the table).

How to delete a partition?
alter table test drop partition p1;

How to add a new partition?
alter table test reorganize partition pdefault into (partition p3 values ​​less than (201901), partition pdefault values ​​less than maxvalue);

How do I check the partitions of a table?
SELECT PARTITION_NAME,TABLE_ROWS FROM information_schema.PARTITIONS WHERE TABLE_NAME='TABLE_NAME';

### Step 3: To consider

* One of the limitations that MySQL has regarding partitions is that the field to be partitioned must be part of the PK or UNIQUE KEY.
* Although conceptually adding a partition to a table does not generate locks, depending on the number of records it can degrade performance.
* MySQL does not create partitions automatically. As a good practice we recommend using a store procedure that creates partitions and another process to delete them. In case you need an example to create the procedures see the attached files (reorganize-partition.txt and drop-partition.txt).
* When dropping partitions, it is always best to run DROP PARTITIONS one at a time. Let's avoid sending the DROP PARTITIONS at once, which makes the engine consider all the drops as a unit and incrementally block the traffic in the tables until the last DROP is finished.

### Step 4: Procedure to add partitions

If you need to add partitions automatically, in all mysql clusters we have a procedure called "add_partition_byrange", basically what it executes is a reorganize of the last partition that we already have (pdefault), (in the previous point we emphasize always having the default partition). For the tables that have this schema defined in their partitions, it is convenient to use this procedure, if you do not find this schema defined and you want to automate the addition of partitions, we recommend that you contact us through fury support.

We show you an example of how to execute the procedure
We have the following table called test_1 with partition pdefault

```MY SQL
CREATE TABLE `test_1` (`id` varchar(10) NOT NULL,`user_id` bigint(5) DEFAULT NULL,`created` datetime NOT NULL, PRIMARY KEY (`id`,`created`)) ENGINE=InnoDB DEFAULT CHARSET=latin1

/*!50100 PARTITION BY RANGE

(extract(year_month from `created`))

(PARTITION old VALUES LESS THAN (201810) ENGINE = InnoDB,

PARTITION p1 VALUES LESS THAN (201811) ENGINE = InnoDB,

PARTITION p2 VALUES LESS THAN (201812) ENGINE = InnoDB,

PARTITION p3 VALUES LESS THAN (201901) ENGINE = InnoDB,

PARTITION p4 VALUES LESS THAN (201902) ENGINE = InnoDB,
```
> To call the procedure you will need 4 values:

* Name of the partitioned table.
* The name of the last partition to modify (in this case it would be pdefault).
* Name of the new partition to add.
* Date range that we want to be inserted into this new partition.
* PARTITION pdefault VALUES LESS THAN MAXVALUE ENGINE = InnoDB) */

> The call of the procedure is done as follows:

![1](https://user-images.githubusercontent.com/81833300/161591500-1be7b64b-cfb5-4f5c-8ba2-8da899d96bf0.png)

Basically what it does is build the query by adding the new p5 partition and generating the pdefault with another date range.

Result:

```MY SQL
CREATE TABLE `test_1` (`id` varchar(10) NOT NULL,`user_id` bigint(5) DEFAULT NULL,`created` datetime NOT NULL, PRIMARY KEY (`id`,`created`)) ENGINE=InnoDB

/*!50100 PARTITION BY RANGE (extract(year_month from `created`))

(PARTITION old VALUES LESS THAN (201810) ENGINE = InnoDB,

PARTITION p1 VALUES LESS THAN (201811) ENGINE = InnoDB,

PARTITION p2 VALUES LESS THAN (201812) ENGINE = InnoDB,

PARTITION p3 VALUES LESS THAN (201901) ENGINE = InnoDB,

PARTITION p4 VALUES LESS THAN (201902) ENGINE = InnoDB,

PARTITION p5 VALUES LESS THAN (201903) ENGINE = InnoDB,

PARTITION pdefault VALUES LESS THAN MAXVALUE ENGINE = InnoDB) */
```
If you have any questions or queries, you can contact us through Fury support :)

Greetings

