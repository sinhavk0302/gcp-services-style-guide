# DBT Coding Standards for BigQuery

This document outlines the coding standards and best practices for developing and managing DBT (Data Build Tool) projects with BigQuery as the data warehouse.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Project Structure](#project-structure)
3. [Model Development](#model-development)
4. [Testing and Validation](#testing-and-validation)
5. [Documentation Standards](#documentation-standards)
6. [Performance Optimization](#performance-optimization)
7. [Security Best Practices](#security-best-practices)
8. [References](#references)

---

## Introduction

DBT is a powerful data transformation tool that enables analysts and engineers to transform, test, and document data in BigQuery. This guide establishes a standard approach to ensure consistent, maintainable, and scalable DBT projects.

---

## Project Structure

1. **Directory Structure**:
   - Use a clear and organized folder structure:
     ```
     dbt_project/
     ├── models/
     │   ├── staging/
     │   ├── marts/
     │   └── intermediate/
     ├── tests/
     ├── macros/
     └── seeds/
     ```

2. **Naming Conventions**:
   - Use lowercase and underscores (`_`) for all names.
   - Prefix staging models with `stg_`, intermediate models with `int_`, and marts with `dim_` or `fact_` depending on use.
     - Example: `stg_sales`, `int_customer_orders`, `dim_customers`.

3. **Version Control**:
   - Maintain the DBT project in a Git repository.
   - Use feature branches for development and follow proper Git workflows (e.g., Git Flow).

---

## Model Development

1. **SQL Formatting**:
   - Use consistent formatting for SQL queries:
     - Keywords in uppercase (e.g., `SELECT`, `FROM`, `WHERE`).
     - Indent fields and clauses for readability.
   - Example:
     ```sql
     SELECT
         customer_id,
         COUNT(order_id) AS order_count
     FROM
         `project.dataset.orders`
     WHERE
         order_status = 'completed'
     GROUP BY
         customer_id
     ```

2. **Model Configuration**:
   - Define configurations at the top of each model file:
     ```sql
     {{ config(
         materialized='view',
         schema='analytics'
     ) }}
     ```

3. **Avoid Hardcoding**:
   - Use DBT variables and Jinja templates for dynamic values:
     ```sql
     SELECT
         *
     FROM
         {{ ref('stg_orders') }}
     ```

4. **Avoid SELECT ***:
   - Always specify the required columns explicitly in the `SELECT` statement.

5. **Incremental Models**:
   - Use incremental models for large datasets:
     ```sql
     {{ config(
         materialized='incremental',
         unique_key='id'
     ) }}
     WHERE
         updated_at > '{{ var("last_run_date") }}'
     ```

---

## Testing and Validation

1. **Testing**:
   - Write tests for all critical models.
   - Use both schema and data tests:
     - Schema Tests: Check for uniqueness, not null, and foreign key relationships.
     - Data Tests: Validate business logic.

   - Example schema test (`schema.yml`):
     ```yaml
     models:
       - name: customers
         columns:
           - name: customer_id
             tests:
               - unique
               - not_null
     ```

2. **Assertions**:
   - Use `dbt test` to validate your models regularly.

3. **CI/CD**:
   - Integrate DBT tests into your CI/CD pipeline to catch issues early.

---

## Documentation Standards

1. **Model Documentation**:
   - Document each model in the `schema.yml` file:
     ```yaml
     models:
       - name: customers
         description: "Contains customer data including demographic information."
     ```

2. **Column Descriptions**:
   - Provide descriptions for all columns:
     ```yaml
     columns:
       - name: customer_id
         description: "Unique identifier for each customer."
     ```

3. **Sources**:
   - Use `sources` to document raw data tables:
     ```yaml
     sources:
       - name: raw
         tables:
           - name: customers
             description: "Raw customer data from the CRM system."
     ```

4. **Data Lineage**:
   - Use the `dbt lineage graph` to visualize dependencies and maintain clarity.

---

## Performance Optimization

1. **Partitioning and Clustering**:
   - Use partitioned and clustered tables in BigQuery for large datasets:
     ```sql
     {{ config(
         materialized='table',
         partition_by={'field': 'created_at', 'data_type': 'timestamp'},
         cluster_by=['customer_id']
     ) }}
     ```

2. **Efficient Queries**:
   - Minimize data scanned by filtering early and selecting only required columns.

3. **Caching**:
   - Leverage BigQuery query results caching to reduce costs.

4. **Review Query Plans**:
   - Use the BigQuery Query Plan to identify and resolve performance bottlenecks.

---

## Security Best Practices

1. **Service Accounts**:
   - Use dedicated service accounts with the principle of least privilege.

2. **Access Control**:
   - Restrict access to datasets and tables using IAM roles.

3. **Encryption**:
   - Ensure all data is encrypted at rest and in transit.

4. **Sensitive Data**:
   - Mask or tokenize sensitive data to comply with data privacy regulations.

---

## References

- [DBT Documentation](https://docs.getdbt.com/)
- [BigQuery Documentation](https://cloud.google.com/bigquery/docs)
- [DBT Best Practices](https://docs.getdbt.com/docs/guides/best-practices)
- [SQL Style Guide](https://www.sqlstyle.guide/)

---

**Maintainers**: Please ensure this document is reviewed and updated periodically to reflect best practices.
