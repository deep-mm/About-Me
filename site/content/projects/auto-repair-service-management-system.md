+++
author = "Deep Mehta"
title = "AUTOR - Auto Repair and Service Management System"
date = "2022-12-10"
description = "This project is an implementation of an car service center application with a primary focus on database design."
tags = [
    "dbms",
    "sql",
    "er-diagram",
    "github",
    "angular",
    "java",
    "devops"
]
+++

[![FeaturedImage](/images/projects/autor_main.png)](https://yoururl.tech/svc)

## Introduction

---

The following activities were performed as part of this project:

1. Designing a Entity-Relationship diagram based on the requirements
2. Convert ER diagram into SQL Tables
3. Develop Java Springboot APIs to interact with the database (Oracle)
4. Setup Triggers, Procedures in SQL to ensure database consistency
5. Develop Angular Frontend to consume APIs

The requirements included, developing a system that allows customers to schedule maintenance and repair services for their cars. Additionally provide interfaces fro store manager, receptionist and mechanics.

## ER Diagram

---

After careful consideration of the requirement document, the following Entity relationship diagram was finalized:

![ER Diagram](/images/projects/autor_er.jpg)

## Converting ER Diagram to SQL

---

The next step was transforming the ER diagram into SQL tables. All the SQL tables that were created as part of this project can be found here [SQL Tables](https://github.com/deep-mm/DBMS-Car-Service-Center/blob/main/sql-files/set_up.sql).

Example: SERVICE_CENTER

```sql

CREATE TABLE SERVICE_CENTER (
    SERVICE_CENTER_ID INTEGER,
    ADDRESS VARCHAR(250) NOT NULL,
    TELEPHONE_NO VARCHAR(15) NOT NULL,
    OPERATIONAL_STATUS INTEGER NOT NULL,
    WEEKEND_WORKING INTEGER NOT NULL,
    MIN_WAGE INTEGER NOT NULL,
    MAX_WAGE INTEGER NOT NULL,
    PRIMARY KEY (SERVICE_CENTER_ID),
    CHECK (OPERATIONAL_STATUS IN (0, 1)),
    CHECK (WEEKEND_WORKING IN (0, 1))
);

```

## Java SpringBoot APIs

---

Next, we developed Java SpringBoot APIs that utilizes JDBC to interact with the Oracle Database. Developing these APIs involved 2 steps:

1. Create Models that exactly represent the tables in Oracle DB (Example: [ServiceCenter.java](https://github.com/deep-mm/DBMS-Car-Service-Center/blob/main/src/main/java/com/dbms/team15/models/ServiceCenter.java))
2. Create SQL queries for CRUD operations and use them in controllers to get or post data (Example: [ServiceCenterController.java](https://github.com/deep-mm/DBMS-Car-Service-Center/blob/main/src/main/java/com/dbms/team15/controllers/ServiceCenterController.java))

All Models & Controllers can be found here: [Models & Controllers](https://github.com/deep-mm/DBMS-Car-Service-Center/tree/main/src/main/java/com/dbms/team15)

## Create SQL Triggers

---

Triggers play an important role in ensuring database consistency and reducing application load. We developed several triggers for our implementation.

Example: CHECK_CUSTOMER_STATUS

```sql

create or replace TRIGGER CHECK_CUSTOMER_STATUS
AFTER
INSERT ON CUSTOMER_CAR FOR EACH ROW BEGIN
UPDATE CUSTOMER C
SET C.status = 1
WHERE C.customer_id = :new.customer_id
    AND C.service_center_id = :new.service_center_id;
END;

```

This trigger ensures that is a customer car is added to the database, the customer status changes to active.

You can find all the triggers here: [Triggers](https://github.com/deep-mm/DBMS-Car-Service-Center/blob/main/sql-files/set_up.sql#L210)

## Angular FrontEnd

---

Final step, was to create a UI for the user to interact with the data. Thus, we created an angular app to consume the java springboot APIs.

The angular project can be found here: [service-center-app](https://github.com/deep-mm/DBMS-Car-Service-Center/tree/main/service-center-app/src)

## Hosting

---

Finally, the entire system was hosted on the cloud to be consumed over the web.

1. Database - Oracle - Hosted on NCSU servers
2. Backend APIs - Java SpringBoot - Hosted on Azure (https://service-center-api.azurewebsites.net)
3. Frontend APP - Angular - Hosted on Azure (https://service-center-app.azurewebsites.net/login)

## DevOps

---

Continuos deployment was setup as part of this project, where the SpringBoot App was directly deployed to Azure App Service, and the Angular app was packaged as a Docker container which is then pulled by Azure App Service.

---

{{< notice info "Project Artifacts & Details" >}}
**Website:** [https://yoururl.tech/svc](https://yoururl.tech/svc)

**API:** [https://service-center-api.azurewebsites.net/](https://service-center-api.azurewebsites.net/)

**Repository** [https://github.com/deep-mm/DBMS-Car-Service-Center](https://github.com/deep-mm/DBMS-Car-Service-Center)

**Technology:** SQL, Java, Angular, Azure, Oracle, GitHub-Actions
{{< /notice >}}
