# BigQuery Standards for Migrating Data from Azure ADLS to GCP

This document provides standards and best practices for designing datasets, tables, views, and other BigQuery objects while migrating data from Azure Data Lake Storage (ADLS) to Google Cloud Platform (GCP).

---

## Table of Contents

1. [Introduction](#introduction)
2. [Dataset Standards](#dataset-standards)
3. [Table Standards](#table-standards)
4. [View Standards](#view-standards)
5. [Access and Permissions](#access-and-permissions)
6. [Performance Optimization](#performance-optimization)
7. [Validation and Monitoring](#validation-and-monitoring)
8. [References](#references)

---

## Introduction

Migrating data from Azure ADLS to GCP requires careful planning and design of BigQuery objects to ensure scalability, performance, and maintainability. This guide establishes standards for datasets, tables, views, and other objects to ensure a seamless migration process.

---

## Dataset Standards

1. **Naming Conventions**:
   - Use descriptive and consistent names in lowercase with underscores (`_`).
   - Format: `project_environment_purpose`. Example: `ecommerce_prod_sales`.

2. **Region Selection**:
   - Create datasets in the same region as the source data or consuming applications.
   - Use multi-regional locations only when necessary.

3. **Labels**:
   - Add labels to datasets for easier organization and cost tracking.
   - Example:
     ```yaml
     labels:
       environment: "prod"
       department: "analytics"
     ```

4. **Dataset Partitioning**:
   - Organize data by creating separate datasets based on business domains or departments.

5. **Retention Policies**:
   - Specify dataset-level retention policies to manage data lifecycle.

---

## Table Standards

1. **Naming Conventions**:
   - Table names should describe the data stored and be in lowercase with underscores.
   - Format: `data_type_timeframe`. Example: `orders_2025`.

2. **Schema Design**:
   - Use clear, descriptive column names in lowercase with underscores.
   - Avoid reserved keywords and special characters.

3. **Partitioning**:
   - Use partitioned tables for large datasets.
   - Prefer `DATE` or `TIMESTAMP` columns for partitioning.

   Example:
   ```sql
   PARTITION BY DATE(created_at)
