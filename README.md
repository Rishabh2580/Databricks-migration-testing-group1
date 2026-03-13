PROJECT TITLE :  Alteryx to Databricks Migration Testing Framework for Retail Sales Analytics

Project Overview : The organization currently processes retail analytics workflows in Alteryx. The company is migrating these workflows to Azure Databricks.

Architecture -:        
                                        
┌──────────────────────────────┐
│        Azure Blob Storage     │
│   (Raw Superstore Dataset)    │
└───────────────┬───────────────┘
                │
                ▼
┌──────────────────────────────────────────┐
│        Databricks Ingestion Notebook     │
│        nb_ingest_superstore_orders       │
│   Reads raw data from Azure Blob Storage │
└───────────────┬──────────────────────────┘
                │
                ▼
┌──────────────────────────────────────────┐
│              Bronze Layer                │
│      Raw Data stored as Delta Table     │
│   capstone_db.bronze_superstore_orders  │
└───────────────┬──────────────────────────┘
                │
                ▼
┌──────────────────────────────────────────┐
│              Silver Layer                │
│        Data Cleaning & Transformation    │
│   capstone_db.silver_superstore_orders  │
└───────────────┬──────────────────────────┘
                │
                ▼
┌──────────────────────────────────────────┐
│               Gold Layer                 │
│        Business Aggregations             │
│        (Category-wise Sales)             │
│     capstone_db.gold_sales_summary       │
└───────────────┬──────────────────────────┘
                │
                ▼
┌──────────────────────────────────────────┐
│            Validation Layer              │
│  ✔ Row Count Validation                 │
│  ✔ Duplicate Record Validation          │
│  ✔ Null Value Validation                │
└───────────────┬──────────────────────────┘
                │
                ▼
┌──────────────────────────────────────────┐
│           Business Validation            │
│  Comparison with Alteryx Output          │
│  File: category_sales_summary.csv        │
└──────────────────────────────────────────┘




Data Processing Layers

Bronze Layer : Raw data is ingested from azure blob storage and stored in a delta table without transformations.

Table_Name : capstone_db.bronze_superstore_orders.

Notebook : nb_ingest_superstore_orders

Silver Layer : Data cleaning and transformation are performed:
- Removed invalid records.
- Data type corrections.
- Basic data quality checks.

  Tabel_Name : capstone_db.silver_superstore_orders

  Notebook : nb_silver_superstore_orders.

  Gold Layer - Business-level aggregations are created to generate insights.

  Aggregations include :

  -Category level sales.
  -Order Counts.

  Table_Name : capstone_db.gold_sales_summary

  Notebook : nb_gold_sales_aggregation



  Data Validation Checks : Validation Checks Performed

  Row Count Validation - Ensures data consistency between bronze and Silver layer.

  Duplicate Validation - Checks duplicate order IDs.

  Null Value Validation - Ensures critical fields do not contain null values.

  NoteBook : nb_data_validation_check


  Business Validation : The final aggregated results are compared with the ALteryx output dataset.

  Comparison performed on:

  -Category level sales.
  -Order Counts.

  Notebook : nb_business_validation

  Final Result -> The aggregated sales result generated in databricks match the alteryx output,confirming a sucessfull migration.

  Technology Used

  -Databricks
  -Pyspark
  -SQL
  -Delta lake
  -Azure blob storage.
  -Github

  Project Structure

  Ingestion
      nb_ingest_superstore_orders

  tranformation
      nb_silver_superstore_orders
      nb_gold_sales_aggregation

  Validation
    nb_data_validation_check
    nb_business_validation

  README.md
    comparison_report
    business_validation_queries
  

  
```
