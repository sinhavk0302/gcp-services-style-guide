# GCP Cloud Composer Style Guide

This document provides guidelines and best practices for working with Google Cloud Composer.

---

## Table of Contents
1. [Introduction](#introduction)
2. [Environment Configuration](#environment-configuration)
3. [DAG Development Standards](#dag-development-standards)
4. [Testing and Monitoring](#testing-and-monitoring)
5. [Security Best Practices](#security-best-practices)
6. [Versioning and Dependency Management](#versioning-and-dependency-management)
7. [References](#references)

---

## Introduction

Google Cloud Composer is a fully managed workflow orchestration service built on Apache Airflow. This guide outlines the standards for configuring, deploying, and maintaining Cloud Composer environments and DAGs (Directed Acyclic Graphs).

---

## Environment Configuration

1. **Environment Naming**: Use descriptive names that reflect the project and purpose. Example: `project-name-team-purpose-env`.
2. **Region Selection**: Deploy environments in regions close to the data source to minimize latency.
3. **Scaling**:
   - Configure appropriate node scaling for workloads (e.g., start with 3 nodes and adjust as needed).
   - Use auto-scaling where possible.
4. **Service Accounts**: Ensure proper IAM roles are assigned to the environment's service account.

---

## DAG Development Standards

1. **DAG Naming**: Use descriptive and consistent names. Example: `data_pipeline_daily`.
2. **Modularization**:
   - Break down complex DAGs into smaller, reusable components.
   - Use custom operators and hooks for repetitive tasks.
3. **Execution Schedule**:
   - Define cron expressions or presets (`@daily`, `@hourly`) clearly.
   - Use time zones explicitly (`start_date=datetime(2023, 1, 1, tzinfo=pytz.UTC)`).
4. **Fail-Safe Mechanisms**:
   - Implement retry policies (`retries=3, retry_delay=timedelta(minutes=5)`).
   - Use SLAs to detect and handle delays.
5. **Code Quality**:
   - Follow PEP 8 standards for Python code.
   - Add comments and documentation for complex logic.

---

## Testing and Monitoring

1. **Unit Testing**:
   - Write unit tests for custom operators and functions using `pytest`.
   - Use the `DagBag` object to validate DAG integrity.
2. **Monitoring**:
   - Set up email or Slack alerts for task failures.
   - Use Airflow's built-in monitoring tools to track DAG performance.

---

## Security Best Practices

1. **Secrets Management**:
   - Use Secret Manager or environment variables to store sensitive data.
   - Avoid hardcoding credentials in DAGs.
2. **Network Security**:
   - Restrict access to the Cloud Composer environment using VPC Service Controls.
   - Enable private IP for the environment.
3. **IAM Policies**:
   - Follow the principle of least privilege for all roles and service accounts.
   - Regularly audit IAM permissions.

---

## Versioning and Dependency Management

1. **Environment Versions**:
   - Use the latest stable Airflow version compatible with your workloads.
2. **Dependency Management**:
   - Use `requirements.txt` to manage Python dependencies.
   - Regularly update dependencies to address security vulnerabilities.

---

## References

- [Google Cloud Composer Documentation](https://cloud.google.com/composer/docs)
- [Apache Airflow Documentation](https://airflow.apache.org/docs/apache-airflow/stable/)
- [PEP 8 – Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/)

---

**Maintainers**: Please ensure this document is reviewed and updated periodically.
