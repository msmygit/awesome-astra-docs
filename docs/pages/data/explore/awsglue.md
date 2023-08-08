---
title: "AWS Glue"
description: "AWS Glue is an ETL (Spark) system to allow you to extract, transform and load data into Amazon datastores (ETL).  By importing Astra data into Glue you can then take the data and push it into Redshift, Sagemaker, or other AWS Services."
tags: "jdbc, data management, ide"
icon: "https://awesome-astra.github.io/docs/img/awsglue/awsglue.svg"
developer_title: "AWSGlue"
developer_url: "https://console.aws.com/"
links:
- title: "Amazon Glue Docs"
  url: "https://docs.aws.amazon.com/glue/index.html"
---

<div class="nosurface" markdown="1">

<details>
<summary><b> 📖 Reference Documentation and Resources</b></summary>
<ol>
<li><a href="https://docs.aws.amazon.com/glue/index.html">AWS Glue Documentation</a>
</ol>
</details>
</div>

## Overview

AWS Glue is a serverless data integration service that makes it easy for analytics users to discover, prepare, move, and integrate data from multiple sources. You can use it for analytics, machine learning, and application development. It also includes additional productivity and data ops tooling for authoring, running jobs, and implementing business workflows.

With AWS Glue, you can discover and connect to more than 70 diverse data sources and manage your data in a centralized data catalog. You can visually create, run, and monitor extract, transform, and load (ETL) pipelines to load data into your data lakes. Also, you can immediately search and query cataloged data using Amazon Athena, Amazon EMR, and Amazon Redshift Spectrum.

- <span class="nosurface">ℹ️ </span>[What is Glue?](https://docs.aws.amazon.com/glue/latest/dg/what-is-glue.html)

DBSchema uses the [Astra JDBC Driver](https://github.com/DataStax-Examples/astra-jdbc-connector/releases/download/5.0/astra-jdbc-connector-5.0.jar) to connect to Cassandra as the storage backend. The Java driver itself supports connections to Astra DB natively.

## Prerequisites

This tutorial will take you through the process of connecting your Astra database to Glue.  This process is somewhat extensive, so please take care to read all of the instructions carefully.

<ul class="prerequisites">
  <li class="nosurface">You should have an <a href="https://astra.dev/3B7HcYo">Astra account</a></li>
  <li class="nosurface">You should <a href="https://awesome-astra.github.io/docs/pages/astra/create-instance/">Create an Astra Database</a></li>
  <li class="nosurface">You should <a href="https://awesome-astra.github.io/docs/pages/astra/create-token/">Have an Astra Token</a></li>
  <li class="nosurface">You should <a href="https://awesome-astra.github.io/docs/pages/astra/download-scb/">Download your Secure bundle</a></li>
  <li class="nosurface">You need an <a href="https://console.aws.amazon.com">AWS account with permissions for S3, IAM, and the AWS Secrets Manager</a>
</ul>



# Step 1 - Setup

## <span class="nosurface">✅ Step 1.1: </span> Create Role in IAM

1. Open [AWS Identity and Access Management](https://us-east-1.console.aws.amazon.com/iamv2/home)
2. In the left hand column, select Select **Roles**

    <img src="https://awesome-astra.github.io/docs/img/awsglue/IAMLeftBar.png" />

3. On the right hand side, click the large blue **Create Role** button

4. For your Trusted entity type, choose  **AWS service**.  In the "Use cases for other AWS Services" type and select "Glue".

5. Select **Next.**

6. On the **Add permissions** page you will need to search for a few different permissions.  You should select the following:
    - AmazonS3FullAccess
    - AWSGlueServiceRole
    - AWSGlueConsoleFullAccess
    - SecretsManagerReadWrite

    <img src="https://awesome-astra.github.io/docs/img/awsglue/IAMLeftBar.png" />

7. On the Name, review, and create page, choose a name for your role (For example purposes I will use AstraGlueRole), then scroll to the bottom of the page and click the blue **Create role** button.

## 1.2 - S3

### <span class="nosurface">✅ Step 1: </span> JDBC Driver

Download [Astra JDBC connector jar](https://github.com/DataStax-Examples/astra-jdbc-connector/releases/download/5.0/astra-jdbc-connector-5.0.jar)  from Github

## 1.3 - Secrets Manager

# Step 2 - Glue Connector

## 2.1 - Connector

## 2.2 - Connection

# Step 3 - Job setup

## 3.1 - Job details

## 3.2 - Source

## 3.3 - Transform

## 3.4 - Test

# Step 4 - Load into Glue Tables 

## 4.1 - Create buckets

## 4.2 - Create database and table

## 4.3 - Add Glue Database target

## 4.4 - Run and test (requires Athena)

### <span class="nosurface">✅ Step 2: </span> Establish the Connection

1. Open [DB Schema](https://dbschema.com/)
2. Select **Connect to the Database**
3. Select **Start**
<img src="https://awesome-astra.github.io/docs/img/dbschema/dbschema-start.png"/>

4. In the **Choose your database** menu, select Cassandra.

5. Select **Next.**
<img src="https://awesome-astra.github.io/docs/img/dbschema/dbschema-cass-sel.png" />

6. Select **JDBC Driver** edit option.  This is the button on the right hand side of the JDBC driver line, with the key icon.
<img src="https://awesome-astra.github.io/docs/img/dbschema/dbschema-connection-d.png" />

7. In the JDBC Driver Manager, select **New**.
8. In the Add RDBMS window, enter **Astra** and select **OK**
<img src="https://awesome-astra.github.io/docs/img/dbschema/dbschema-driver-manager.png" />

9. Select **OK** in the confirmation message.
<img src="https://awesome-astra.github.io/docs/img/dbschema/dbschema-connection.png" />

10. Upload the Astra JDBC Driver.
11. Select **Open**
12. Once you upload the Astra JDBC Driver, you will see **Astra** in the **Choose your Database** window. Select **Next**.

<img src="https://awesome-astra.github.io/docs/img/dbschema/dbschema-astra-config.png" height="500px" />

13. In the connection window, select the JDBC Driver "astra-jdbc-connector-5.0.jar com.datastax.astra.jdbc.AstraJdbcDriver.  Under JDBC URL select "Edit Manually".
 
14. In the Astra Connection Dialog, add JDBC URL as
    ```bash
    jdbc:astra://<database_name>/<keyspace_name>?token=<application_token>
    ```
    with the following variables:

       - **database_name:** The name or ID for the database you want to connect to
       - **keyspace_name:** The keyspace you want to use
       - **application_token:** Generated from Astra DB console. See [Manage application tokens.](https://docs.datastax.com/en/astra/docs/manage-application-tokens.html)
    

14. Select **Connect**
<img src="https://awesome-astra.github.io/docs/img/dbschema/dbschema-url.png" height="500px" />

15. In the **Select Schemas/Catalogs**, select the keyspace to which you want to connect.
16. Select **OK.**
<img src="https://awesome-astra.github.io/docs/img/dbschema/dbschema-connetion-established.png" height="500px" />

### <span class="nosurface">✅ Step 3: </span> Final Test

Now that your connection is working, you can create tables, introspect your keyspaces, view your data in the DBSchema GUI, and more.

To learn more about DBSchema, see [Quick start with DBSchema](https://dbschema.com/tutorials.html)

<div class="nosurface" markdown="1">
[🏠 Back to HOME](https://awesome-astra.github.io/docs/) 
</div>