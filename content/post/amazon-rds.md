+++
author = "Krishnan S"
title = "Amazon RDS"
date = "2021-04-17"
description = "Setup PostgresSQL database using RDS"
categories = [
  "rds",
  "aws"
]
aliases = []
+++

Amazon RDS is a service from AWS which allows us to setup and operate different types of Relational Databases with ease.
<!--more-->

While picking a database for my projects more often than not I go with MongoDB. The reason being Atlas offers a simple and cheap hosting solution to create and manage them. So when I decided to use PostgresSQL for one project, I started looking at available cloud hosting providers and stumbled upon **Amazon RDS**


RDS supports different database engines including PostgresSQL, MySQL, Oracle etc. The main advantage of using a service like RDS is database administration tasks like backups, monitoring, performance insights are handled out of the box so we can focus on building our applications.

### Create and Configure

To create a new database in RDS, we go to AWS console and select RDS from the services menu and choose **Create Database** which takes us to the initial configuration screen.

RDS provides us wiht two ways to configure a DB, *Standard Create* -  manually choose each config options or *Easy Create* - go with recommended config options. Let's explore each of these options.

#### 1. Engine options.

Since RDS supports multiple database engines, we have to select our preferred engine and the corresponding version. I'm going with <mark>PostgresSQL 13.2</mark>

![image engine-types](/assets/img/engine-type.png)

#### 2. Templates

Here we need to decide from three available options.
* Production -  High performance and availability
* Dev/Test -  Use for development or staging environments
* Free Tier -  Use for POCs and exploring

#### 3. Settings

We have to provide a name for our database instance and also configure authentication details like username and password.

![image settings](/assets/img/settings.png)

#### 4. Instance Size and Storage

Next, we select the instance type and storage. This is dependent entirely on the use case and requirements. For list of available instance types and pricing refer [Amazon RDS Pricing](https://aws.amazon.com/rds/postgresql/pricing).

#### 5. Availability

If we want our database deployment to be highly available and have data redundancy we can create a replica in a different Availablity Zone. Since a replica incurs additional charges, Multi AZ deployments is typically used for production environments

#### 6. Connectivity

This is where we configure how we are going to connect with our RDS Database instance. We can select an existing VPC or create new VPC. Another important choice is if we want to allow public access to our database or restrict access to only instances within the VPC. 

![image connectivity](/assets/img/connectivity.png)

Finally, we can check the estimated monthly costs for our selected configuration and click on **Create Database** to create the RDS instance!