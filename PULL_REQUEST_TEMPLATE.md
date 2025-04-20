# Pull Request Title

## Description
Provide a clear and concise description of the changes introduced by this pull request.

- What problem does this solve?
- What features or enhancements are added?

---

## Checklist
### General
- [ ] **Code Formatting**: Is the code formatted correctly and adheres to the style guide?
- [ ] **Documentation**: Are the relevant documents, README, or inline comments updated?
- [ ] **Testing**: Are unit tests, integration tests, or other relevant tests included and passing?

---

### Service-Specific Checklist
### Cloud Composer Checklist
#### DAGs
- [ ] DAGs pass validation using `airflow dags validate`.
- [ ] DAG names are descriptive, follow naming conventions, and align with team standards.
- [ ] DAG structure is modular and tasks are logically organized.
- [ ] Task dependencies are clearly defined, with no circular dependencies.
- [ ] Retries, SLAs, and schedules are appropriately configured for each DAG.
- [ ] DAG parameters and default arguments are consistent and well-documented.

#### Security
- [ ] Environment variables, secrets, and connection credentials are securely managed (e.g., using Secret Manager or environment configurations).
- [ ] GCP IAM roles and permissions follow the principle of least privilege.
- [ ] DAGs avoid hardcoding sensitive data or credentials.

#### Code Quality
- [ ] Python code adheres to PEP 8 standards and is modularized for readability and reusability.
- [ ] External libraries and dependencies in `requirements.txt` are version-locked and audited for vulnerabilities.
- [ ] DAGs and Python scripts are optimized for performance, avoiding unnecessary overhead.

#### Observability
- [ ] Logging is implemented at appropriate levels (INFO, DEBUG, ERROR) for all tasks.
- [ ] Monitoring and alerting mechanisms (e.g., Stackdriver alerts) are configured for critical tasks.
- [ ] DAG execution success and failure scenarios are logged and reviewed.

#### Testing
- [ ] DAGs are tested with mock data for both positive and negative scenarios.
- [ ] Python scripts and custom operators, if any, have associated unit tests.
- [ ] Test cases for edge scenarios and failure handling are included.

#### Performance
- [ ] DAG task execution times are reviewed and optimized where possible.
- [ ] Parallelization and task batching are implemented where applicable.
- [ ] External API and database calls within tasks are optimized for efficiency.

---
#### BigQuery
- [ ] SQL queries are optimized and reviewed for performance (e.g., using query execution plans).
- [ ] Dataset permissions follow the principle of least privilege.
- [ ] Table schemas are appropriately versioned and documented.

#### Dataproc
- [ ] Cluster configurations (e.g., machine types, autoscaling policies) are appropriate for the workload.
- [ ] Jobs are tested and validated for successful execution.
- [ ] Usage of custom initialization actions or startup scripts is documented.

#### DBT (Data Build Tool)
- [ ] DBT models are tested with appropriate `tests` and `sources`.
- [ ] Model dependencies are clearly defined in `dbt_project.yml`.
- [ ] Naming conventions for models and folders adhere to the team's standards.

#### Dataflow
- [ ] Pipeline logic is modular, readable, and well-documented.
- [ ] Resource configurations (e.g., worker types, autoscaling) are cost-optimized.
- [ ] Monitoring and logging mechanisms (e.g., Stackdriver Logs) are set up and verified.

#### Cloud Storage
- [ ] Bucket permissions are reviewed and follow security best practices.
- [ ] Object lifecycle policies (e.g., retention, archival) are configured as needed.
- [ ] Storage class selection aligns with the use case (e.g., standard, nearline, coldline).

#### Pub/Sub
- [ ] Topic and subscription configurations (e.g., acknowledgment deadlines, retry policies) are appropriate.
- [ ] Dead-letter topics are configured for error handling, if applicable.
- [ ] Subscriber code is tested for message acknowledgment and idempotency.

---

## Additional Notes
Add any additional information that might help the reviewer.

---

## Reviewer Checklist
- [ ] Are all comments addressed?
- [ ] Is the code ready to be merged?
