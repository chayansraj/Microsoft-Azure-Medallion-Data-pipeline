# Data Migration and Analytics using Microsoft Azure (Data Engineering)
In this project we are going to create an end-to-end data platform right from Data Ingestion, Data Transformation, Data Loading and Reporting.

# Project Goals 

1. Data Ingestion - Create a data ingestion pipeline to extract data from on-premises SQL Server Database using Azure Data Factory
2. Data Storage - Create a centralized repository to store data from SQL Server Database into Azure Data Lake Gen 2 storage.
3. Data Transformation - Create ETL job to extract the data, do simple transformations and load the clean data using Azure Databricks.
4. Data Governance - Create Azure key vaults and Active Directory to monitor and govern the whole project using Azure roles.
5. Data Analytics - Create data integration pipeline with Power BI using Azure Synapse Analytics to create powerful visualizations.


# Data Architecture

The architecture (Data flow) used in this project uses different Azure functionalities.

<p align="center">
  <img width="950" height="550" src="https://github.com/chayansraj/Microsoft-Azure-Data-Engineering-End-to-End/assets/22219089/35edfd98-87ae-4389-81f0-40d1b7021892">
  <h6 align = "center" > Source: Author </h6>
</p>

# Dataset Used 
The dataset is an open source database provided by Microsoft namely 'AdventureWorks2017'. It contains a lot of different tables with their corresponding relationships. Dataset link - https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms

# Microsoft Azure Services used in this project
1. **Azure Data Lake Gen2 Storage** - A data lake is a single, centralized repository where you can store all your data, both structured and unstructured. It provides various tools to deal with Big Data analytics based on Azure Blob Storage. It is mainly designed to work with Hadoop and all frameworks that use the Apache HDFS as their data access layer.
2. **Azure Data Factory** - ADF is a fully managed, serverless data intergration service. It allows to create Data Pipelines to Extract, Transform and Load (ELT) data from more than 90 sources. It allows us to choose from more than 90 built-in connectors to acquire data from big data sources such as Amazon Redshift, Google BigQuery, and HDFS.
3. **Azure Databricks** - It is a cloud-based big data analytics platform provided by Microsoft Azure, built on top of Apache Spark. Azure Databricks is a fully managed first-party service that enables an open data lakehouse in Azure. Jupyter notebooks can be used to transform, perform analytics, machine learning, etc. offering the capabilities of Apache Spark.
4. **Azure Synapse Analytics** - Azure Synapse Analytics, formerly known as Azure SQL Data Warehouse, is a cloud-based analytics service provided by Microsoft Azure. It's designed to handle large volumes of data and enable organizations to perform data warehousing, big data analytics, and data integration tasks. It offers a distributed architecture to perform big data analytics.
5. **Azure Key Vault** - Azure Key Vault is a cloud service offered by Microsoft Azure that allows you to securely manage cryptographic keys, secrets, certificates, and other sensitive information used by your applications and services. Key Vault provides a centralized and secure way to store and control access to these sensitive materials.
6. **Azure Active Directory** - Azure Active Directory (Azure AD) is Microsoft's cloud-based identity and access management service. It provides a comprehensive set of capabilities for managing identities, securing access to resources, and enabling seamless authentication and authorization across applications and services. Azure AD is a foundational component of Microsoft's cloud services and plays a crucial role in modern IT infrastructure.
7. **Microsoft Power BI** - Microsoft Power BI is a powerful business intelligence (BI) platform that allows users to visualize and share insights from their data. It enables organizations to connect to a wide range of data sources, transform and shape the data, create interactive reports and dashboards, and share those insights with others. Power BI is designed to help users make data-driven decisions and gain actionable insights from their data.

# Implementation
* **Step 1** - Create a data integration link service to connect SQL server with Azure Data Factory
  Since, the database is located in an on-premises SQL Server, Microsoft Azure needs a way to detect the stored data and able to interact with it. To actualize that, the first step includes c       creating a Self Hosted Integration Runtime (SHIR) linked service and install it on the physical machine where the server is deployed. 

<p align="center">
  <img width="500" height="350" src="https://github.com/chayansraj/Microsoft-Azure-Data-Engineering-End-to-End/assets/22219089/209c6c93-b4ad-4a54-bea5-42e4c02e0e0f">
  <h6 align = "center" > Source: Author </h6>
</p>

Start the installed integration runtime and ADF is ready to be integrated with On-prem SQL Server Database. Create a new pipeline in ADF to copy data from SQL Server to Azure Data Lake Storage Gen2. It is important to select the Source and Sink properties to define the correct data flow. The pipeline consists of two parts, firstly, the lookup table that will query the name and schema of each table stored in the SQL Server Database. Secondly, creating a ForEach element that runs a for-loop through the output of lookup table activity and store it in bronze storage layer which is exact copy of the SQL database. The folder structure is supposed to look like Layer/Schema/TableName/TableName.parquet

<p align="center">
  <img width="400" height="250" src="https://github.com/chayansraj/Microsoft-Azure-Data-Engineering-End-to-End/assets/22219089/a290089c-66cf-404d-951c-cc59979c4803">
  <h6 align = "center" > Source: Author </h6>
</p>







