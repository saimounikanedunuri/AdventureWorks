Azure Data Engineering Project Documentation

Data Architecture

Data Source: Fetching data from API

Azure Data Factory: Orchestration tool used to pull source data and land it in the bronze layer. Activities performed include:

Building static and dynamic pipelines

Using parameters

Implementing loops

Utilizing lookup activities

Medallion Architecture

Data traverses through three different zones:

Raw Layer (Bronze): Stores data as-is from the source.

Transform Layer (Silver): Data is transformed and pushed from the bronze layer to the silver layer.

Serving Layer (Gold): Data is served to stakeholders (analysts, data scientists) using Power BI dashboards.

Dataset: Adventure Works

Steps to Create Resources and Implement Pipelines:
-------------------------------------------------

Creating a Resource Group

Use tags to categorize resources (optional).

Create a Data Lake (Storage Account)

Set redundancy to LRS (Local Redundant Storage).

Enable hierarchical namespace for Data Lake functionality.

Difference between Blob and Data Lake:
-------------------------------------

Blob: Does not support folder hierarchy.

Data Lake: Supports folder hierarchy.

Create Azure Data Factory

Navigate to the Author tab for pipeline creation.

Use the Monitor tab to check pipeline status and debug errors.

Use the Manage tab for repositories, GitHub, and DevOps connections.

Build blocks such as pipelines, activities, functions, notebooks.

Create Containers in Data Lake

Create containers for bronze, silver, and gold layers.

Load data into the bronze layer using linked services.

Create Linked Services

First Linked Service: HTTP

Second Linked Service: ADLS GEN2 (Data Lake Storage)

Test connections to ensure they are established correctly.

Create Datasets

For the source:

Format: CSV

Linked service: HTTP

Provide relative URL and set the first row as the header.

For the sink:

Format: CSV

Linked service: ADLS GEN2

Static Pipeline Implementation

Use Copy Activity to load data from the source to the sink.

Debug and publish the pipeline.

Dynamic Pipeline Implementation

Create parameterized datasets to handle multiple files.

Use JSON to iterate over file names and store them in a new container.

Implement Lookup Activity to view file outputs.

Storage Access via Entra ID

Navigate to Entra ID and create an app registration.

Store the client secret and assign roles for read/write access.

Phase 2: Transformations and Databricks Integration
---------------------------------------------------

Databricks Setup

Create a Databricks resource in Azure.

Launch the Databricks UI and create a compute cluster.

Use Databricks to ingest data from the raw layer into the silver layer with transformations.

Assign Roles and Access

Assign roles in the Azure portal for secure access.

Configure Databricks to connect to the storage account and process data dynamically.

Phase 3: Serving Layer in Synapse Analytics
--------------------------------------------

Synapse Workspace Setup

Create a Synapse workspace in the resource group.

Use the existing storage account created earlier.

Synapse supports integration with Azure Data Factory, Spark, and SQL Data Warehouse.

Synapse Components:
------------------

Azure Data Factory: Integrate pipelines.

Spark Pools: Perform transformations.

SQL Data Warehouse: Create and manage dedicated and serverless databases.

Data Warehouse Creation

Create a dedicated SQL database for structured storage.

Use serverless options for lakehouse architecture (data stored in Data Lake with metadata).

Implement OPENROWSET() for querying raw data in the lake.

Data Processing

Create credentials to connect to the storage account.

Use managed identity, SAS tokens, or access keys.

Define external data sources and file formats:

External Data Source: Points to the container (e.g., silver container).

External File Format: Defines the file format (CSV, Parquet, JSON).

Create views for transformed data in the gold layer.

Use CTAS (Create Table As Select) to create external tables from views for long-term storage.

Connecting Synapse to Power BI

Establish a connection between Synapse and Power BI using SQL endpoints.

Build Power BI dashboards using data in the gold layer.

Project Overview:
-----------------

Loaded data into the bronze layer using HTTP.

Processed and transformed data in Databricks from the bronze to the silver layer.

Pulled data from the silver layer into Synapse, created views, and pushed data into the gold layer.

Established a connection with Power BI for visualization and reporting.

Status:
-------

Raw Data Ingestion: Completed

Dynamic Data Processing: Successfully implemented

Databricks Configuration: Completed for raw to silver layer transformations

Serving Layer: Completed with Synapse Analytics

Power BI Dashboards: Successfully connected and operational

