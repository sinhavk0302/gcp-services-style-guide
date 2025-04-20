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
#### Composer
- [ ] DAGs are tested for validity using `airflow dags validate`.
- [ ] Environment variables and connections are securely managed (e.g., using Secret Manager).
- [ ] Dependencies in `requirements.txt` are well-defined and version-locked.

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
