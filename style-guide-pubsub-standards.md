# GCP Pub/Sub Style Guide

This document provides guidelines and best practices for using Google Cloud Pub/Sub to build reliable, scalable, and maintainable messaging systems.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Topic and Subscription Configuration](#topic-and-subscription-configuration)
3. [Message Publishing](#message-publishing)
4. [Message Consumption](#message-consumption)
5. [Error Handling and Retries](#error-handling-and-retries)
6. [Security Best Practices](#security-best-practices)
7. [Monitoring and Logging](#monitoring-and-logging)
8. [References](#references)

---

## Introduction

Google Cloud Pub/Sub is a fully managed messaging service that enables asynchronous communication between services. This guide outlines the standards for creating and managing topics, subscriptions, and messages.

---

## Topic and Subscription Configuration

1. **Naming Conventions**:
   - Use descriptive and consistent names for topics and subscriptions. Examples:
     - Topic: `project-name-environment-event-type` (e.g., `ecommerce-prod-order-created`)
     - Subscription: `project-name-environment-processor` (e.g., `ecommerce-prod-order-processor`).

2. **Topic Design**:
   - Use a separate topic for each distinct type of event.
   - Avoid using a single topic for unrelated events.

3. **Subscription Types**:
   - Use **pull** subscriptions for backend systems and batch processing.
   - Use **push** subscriptions for event-driven architectures where immediate processing is required.

4. **Dead Letter Topics (DLT)**:
   - Configure a Dead Letter Topic for subscriptions to handle undeliverable messages.
   - Define a maximum delivery attempt threshold before messages are sent to the DLT.

5. **Retention Policies**:
   - Set an appropriate message retention duration (default is 7 days).
   - Use shorter retention durations for high-throughput systems to save costs.

---

## Message Publishing

1. **Message Structure**:
   - Use JSON as the message format for interoperability.
   - Include metadata in message attributes (e.g., `eventType`, `sourceSystem`, `timestamp`).

2. **Message Size**:
   - Keep messages small (max 10 MB) to avoid performance issues.
   - Use references to large data stored in Google Cloud Storage instead of embedding it in the message.

3. **Batch Publishing**:
   - Use batch publishing to reduce API calls and improve performance.

4. **Ordering**:
   - Enable message ordering where event sequence matters.
   - Use ordering keys to group related messages.

---

## Message Consumption

1. **Acknowledgement**:
   - Acknowledge messages only after successful processing to prevent message loss.
   - Use manual acknowledgment for fine-grained control.

2. **Concurrency**:
   - Use parallel processing to improve throughput.
   - Limit the number of concurrent consumers to avoid overwhelming downstream systems.

3. **Idempotency**:
   - Ensure message processing is idempotent to handle duplicate deliveries.

4. **Backoff Policies**:
   - Implement exponential backoff for retrying failed messages.
   - Use the Pub/Sub backoff settings for push subscriptions.

---

## Error Handling and Retries

1. **Dead Letter Topics**:
   - Configure Dead Letter Topics to capture undeliverable messages.
   - Regularly monitor and process messages in the DLT.

2. **Retry Logic**:
   - Use exponential backoff for retries to prevent overloading the system.
   - Customize retry settings based on message criticality.

3. **Poison Messages**:
   - Detect and isolate poison messages (messages that always fail).
   - Use Dead Letter Topics or specific logging to analyze and resolve issues.

---

## Security Best Practices

1. **IAM Roles**:
   - Use predefined roles such as `roles/pubsub.publisher` and `roles/pubsub.subscriber`.
   - Follow the principle of least privilege for all Pub/Sub roles.

2. **Authentication**:
   - Use service accounts for accessing Pub/Sub resources.
   - Avoid using user credentials in production environments.

3. **Encryption**:
   - Use server-side encryption (enabled by default).
   - For sensitive data, use Customer-Managed Encryption Keys (CMEK).

4. **Audit Logging**:
   - Enable Cloud Audit Logs for Pub/Sub to monitor access and actions.

---

## Monitoring and Logging

1. **Monitoring**:
   - Use Cloud Monitoring to track metrics such as message backlog, delivery latency, and error rates.
   - Set up alerts for high message backlog or processing failures.

2. **Logging**:
   - Enable logging for message acknowledgments, errors, and retries.
   - Use structured logging for easier analysis.

3. **Tracing**:
   - Use Cloud Trace to track message flows across distributed systems.

---

## References

- [Google Cloud Pub/Sub Documentation](https://cloud.google.com/pubsub/docs)
- [Pub/Sub Best Practices](https://cloud.google.com/pubsub/docs/best-practices)
- [IAM Roles for Pub/Sub](https://cloud.google.com/pubsub/docs/access-control)
- [Cloud Monitoring for Pub/Sub](https://cloud.google.com/pubsub/docs/monitoring)

---

**Maintainers**: Please ensure this document is reviewed and updated periodically.
