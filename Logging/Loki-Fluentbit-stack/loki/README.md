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
















