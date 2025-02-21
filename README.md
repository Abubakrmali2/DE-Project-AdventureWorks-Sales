![ToolsOver](https://github.com/Abubakrmali2/DE-Project-AdventureWorks-Sales/blob/main/Images/Untitled-2024-01-27-1406.png)

# Azure End-To-End Data Engineering Project - AdventureWorks Sales Analysis

---

## Introduction

Welcome to the Azure Data Engineering project! This project demonstrates building an end-to-end data pipeline to analyze and derive insights from the AdventureWorks sales dataset.  We leverage modern data engineering and analytics techniques using various Azure services.

## Overview

This project focuses on building a dynamic, end-to-end pipeline using Azure technologies.  We ingest, process, analyze, and visualize the AdventureWorks sales data, employing a medallion architecture for data storage.  This architecture helps organize the data into different layers (Bronze, Silver, Gold) for varying levels of processing and refinement.

## Project Goals 

*   Ingest data dynamically from [Github as Source of AdventureWorks dataset as CSV files]
*   Transform and cleanse the data for analysis.
*   Store the data in a medallion architecture (Bronze, Silver, Gold layers).
*   Perform data analysis and generate insights.
*   Visualize the insights using [Power BI].
  

## Technologies Used 

*   **Data ingestion and Orchestration:** Azure Data Factory.
*   **Data Storage:** Azure Blob Storage (for raw data/Bronze layer), Azure Data Lake Storage Gen2 (recommended for Silver/Gold layers for performance and hierarchical namespace).
*   **Data Processing /Transformation Azure Databricks.
*   **Data Lakehouse:** Azure Synapse Analytics  
*   **Data Visualization:**  Power BI.

## Project Architecture
![ToolsOver](https://github.com/Abubakrmali2/DE-Project-AdventureWorks-Sales/blob/main/Images/Untitled-2024-01-27-1406.png)


## Data Flow

This section describes the flow of data through the pipeline, from ingestion to visualization.

1.  **Ingestion:** Data is ingested dynamically from CSV files stored in a GitHub repository using Azure Data Factory. A JSON parameter file drives the ingestion process, enabling flexible and automated data loading from the specified folder within the repository.

2.  **Bronze Layer (Raw Data):** The raw data, in its original CSV format, is stored in the Bronze layer within **Azure Data Lake Storage Gen2**. This layer acts as the source of truth, preserving the data in its original state for future reprocessing or auditing.

3.  **Silver Layer (Cleaned and Transformed Data):** Azure Databricks is used to process the data from the Bronze layer. The following transformations are performed:
    *   Creation of a Calendar table.
    *   Removal of duplicate records.
    *   Concatenation and splitting of columns.
    *   Replacement of values.
    The transformed data is then written to the Silver layer in Parquet format within **Azure Data Lake Storage Gen2**.

4.  **Gold Layer (Aggregated and Modeled Data):** Azure Synapse Analytics (specifically, the *serverless SQL pool*) is used to create aggregated and modeled data, ready for reporting and analysis. This is achieved by defining views and external tables over the Parquet files in the Silver layer (and potentially performing further aggregations within the serverless SQL pool itself). The Gold layer data is then stored in **Azure Data Lake Storage Gen2**.

5.  **Analysis and Visualization:** Power BI is connected to the Azure Synapse Analytics serverless SQL pool. This connection allows Power BI to query the aggregated and modeled data in the Gold layer, enabling the creation of informative reports with valuable insights.


<iframe title="Aw-Sales_report" width="600" height="373.5" src="https://app.powerbi.com/view?r=eyJrIjoiYzcxMDBiMjItMGRjYi00NDc5LWJmNzQtYmNjZGYyNzM2YWU4IiwidCI6IjcyZTFhYTg1LTI5NjMtNDk3Yi1hOThhLWQ5MDk5M2ZiMDQ2NiIsImMiOjl9" frameborder="0" allowFullScreen="true"></iframe>
