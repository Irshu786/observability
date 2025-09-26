## The basic setup of loki stack - simple scalable setup

loki-canary
loki-chunks-cache
loki-compactor
loki-distributor, loki-distributor-headless
loki-gateway
loki-index-gateway, loki-index-gateway-headless
loki-ingestor
loki-ingestor-zone-a-headless
loki-ingestor-zone-b-headless
loki-ingestor-zone-c-headless
loki-memberlist
loki-querier
loki-query-frontend, loki-query-frontend
loki-query-scheduler
loki-results-cache
loki-ruler


-- To nake the setup available with basic checks 

1. Disable auth
362 - { auth_enabled: false }
2. loki_configs to improve performance
ingestion_rate_strategy: local
per_stream_rate_limit: 500M
per_stream_rate_limit_burst: 900M
ingestion_rate_mb: 800
ingestion_burst_size_mb: 900
max_global_streams_per_user: 0
max_line_size: 0

3. UI enabled: true
4. lokiCanary: Kind: Deployment [ If required, keep Daemonset ]
5. enableIPV6: false [ Not required of ipv6 ]










# Loki Stack Setup (Basic & Scalable)

This guide provides a simple and scalable setup for deploying **Loki** — a log aggregation system that integrates well with **Grafana**. The setup includes components necessary for scaling, with optimizations for performance and basic checks to ensure the system is up and running.

---

## Table of Contents

1. [Introduction](#introduction)  
2. [Basic Configuration](#basic-configuration)  
3. [Loki Components](#loki-components)  
   - [loki-canary](#loki-canary)  
   - [loki-chunks-cache](#loki-chunks-cache)  
   - [loki-compactor](#loki-compactor)  
   - [loki-distributor, loki-distributor-headless](#loki-distributor-loki-distributor-headless)  
   - [loki-gateway](#loki-gateway)  
   - [loki-index-gateway, loki-index-gateway-headless](#loki-index-gateway-loki-index-gateway-headless)  
   - [loki-ingestor](#loki-ingestor)  
   - [loki-ingestor-zone-a-headless, zone-b-headless, zone-c-headless](#loki-ingestor-zone-a-headless-zone-b-headless-zone-c-headless)  
   - [loki-memberlist](#loki-memberlist)  
   - [loki-querier](#loki-querier)  
   - [loki-query-frontend](#loki-query-frontend)  
   - [loki-query-scheduler](#loki-query-scheduler)  
   - [loki-results-cache](#loki-results-cache)  
   - [loki-ruler](#loki-ruler)  
4. [Configuration Details](#configuration-details)  
   - [Auth Configuration](#auth-configuration)  
   - [Performance Settings](#performance-settings)  
   - [UI Settings](#ui-settings)  
5. [Deployment Instructions](#deployment-instructions)  
6. [Troubleshooting](#troubleshooting)  

---

## Introduction

Loki is a highly scalable log aggregation system designed for efficiency and flexibility. This setup involves configuring the Loki components for high availability, ensuring scalability, and optimizing performance. This guide walks you through each component of the Loki stack and their configurations for a basic yet robust deployment.

---

## Basic Configuration

To ensure a smooth setup, we recommend the following configurations:

1. **Disable Auth**  
   - Setting: `{ auth_enabled: false }`  
   - Reason: For basic setups, authentication is often not required, simplifying access control.

2. **Loki Performance Optimizations**  
   These configurations help improve the overall performance:
   ```yaml
   ingestion_rate_strategy: local
   per_stream_rate_limit: 500M
   per_stream_rate_limit_burst: 900M
   ingestion_rate_mb: 800
   ingestion_burst_size_mb: 900
   max_global_streams_per_user: 0
   max_line_size: 0

# Loki Stack Setup (Basic & Scalable)

This guide provides a simple and scalable setup for deploying **Loki** — a log aggregation system that integrates well with **Grafana**. The setup includes components necessary for scaling, with optimizations for performance and basic checks to ensure the system is up and running.

---

## UI Settings

- **UI enabled:** `true`  
  Enables the Grafana UI for log visualization.

---

## Deployment Type

- **lokiCanary:** Deployment is preferred.  
  You can opt for DaemonSet if required for specific environments (e.g., Kubernetes).

---

## IPV6

- Set `enableIPV6: false` if you do not need IPv6 support.

---

## Loki Components

### loki-canary
- **What it is:** This component is used for checking the health of the Loki cluster.  
- **Why it’s used:** Ensures the basic functionality and availability of Loki components before routing real traffic. Acts as a simple smoke test for deployment.

### loki-chunks-cache
- **What it is:** A cache for storing chunks of logs.  
- **Why it’s used:** Helps to speed up the retrieval of logs by caching chunks, reducing access latency and improving performance.

### loki-compactor
- **What it is:** The compactor component merges smaller stored log chunks over time.  
- **Why it’s used:** Optimizes storage by compacting data, reducing storage overhead and improving query performance.

### loki-distributor, loki-distributor-headless
- **What it is:** Distributes incoming log streams to multiple ingestors.  
- **Why it’s used:** Ensures efficient and balanced distribution of logs across ingestor instances. The headless service version supports Kubernetes StatefulSets.

### loki-gateway
- **What it is:** Handles incoming requests and routes them appropriately.  
- **Why it’s used:** Acts as an entry point, improving scalability and flexibility of the Loki architecture.

### loki-index-gateway, loki-index-gateway-headless
- **What it is:** Manages index storage and queries.  
- **Why it’s used:** Facilitates efficient querying by managing index data crucial for log retrieval.

### loki-ingestor
- **What it is:** Stores logs into persistent storage.  
- **Why it’s used:** Responsible for the actual log persistence, ensuring data is saved and retrievable.

### loki-ingestor-zone-a-headless, zone-b-headless, zone-c-headless
- **What it is:** Ingester instances distributed across multiple zones.  
- **Why it’s used:** Provides fault tolerance and high availability by distributing log ingestion across zones.

### loki-memberlist
- **What it is:** Manages cluster membership and service discovery.  
- **Why it’s used:** Enables components to discover and communicate with each other, maintaining cluster health.

### loki-querier
- **What it is:** Processes log queries from users, fetching data from ingestors and indexes.  
- **Why it’s used:** Core component for retrieving logs and serving query results to Grafana.

### loki-query-frontend
- **What it is:** Intermediary that optimizes and balances queries before reaching the querier.  
- **Why it’s used:** Improves query performance via sharding, caching, and load balancing.

### loki-query-scheduler
- **What it is:** Manages scheduling and execution of queries.  
- **Why it’s used:** Ensures efficient query execution to reduce latency and resource contention.

### loki-results-cache
- **What it is:** Caches query results to speed up repeated queries.  
- **Why it’s used:** Enhances performance by reducing backend load on frequent queries.

### loki-ruler
- **What it is:** Runs rules and generates alerts based on log data.  
- **Why it’s used:** Automates monitoring by triggering alerts on specific log conditions.

---

## Configuration Details

### Auth Configuration

Disable authentication for basic setups to simplify deployment:

```yaml
auth_enabled: false






