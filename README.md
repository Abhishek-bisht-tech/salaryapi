# Salary API Documentation

<img width="296" height="283" alt="Screenshot from 2025-11-21 13-31-07" src="https://github.com/user-attachments/assets/82ce868c-1f43-4c02-b1b2-959314816a7d" />


## Author Table

| **Author** | **Created on** | **Version** | **Last updated by** | **Last Edited On** | **Pre Reviewer** | **L0 Reviewer** | **L1 Reviewer** | **L2 Reviewer** |
|-----------|----------------|-------------|----------------------|--------------------|------------------|------------------|------------------|------------------|
| Abhishek  | 21-11-2025     | 1.0         | Abhishek             | 21-11-2025         |                  |                  |                  |                  |

---

## Table of Contents  
- [Introduction](#introduction)  
- [Key Features](#key-features)  
- [Pre-requisites](#pre-requisites)

  - [Build Time Dependencies](#build-time-dependencies)  
  - [Run Time Dependencies](#run-time-dependencies)  
  - [Other Dependencies](#other-dependencies)  

- [Important Ports](#important-ports)  
- [Architecture](#architecture)  
- [Dataflow Explanation](#dataflow-explanation)  
- [Installation Guide](#installation-guide)  
- [Disaster Recovery](#disaster-recovery)  
- [High Availability](#high-availability)  
- [Troubleshooting](#troubleshooting)  
- [Contact Information](#contact-information)  
- [References](#references)

---

## Introduction
Salary API is a Java-based microservice responsible for managing salary-related transactions and records inside the OT-Microservices ecosystem. It is platform independent and requires Java Runtime to execute. The service supports ScyllaDB, Redis, Swagger, Prometheus, OpenTelemetry, and uses migrate for database migrations.

---

## Key Features

| Feature | Description |
|--------|-------------|
| **Spring Boot Framework** | Uses embedded Tomcat server. |
| **ScyllaDB Storage** | Stores all salary data. |
| **Redis Caching** | Improves performance by caching frequent requests. |
| **Prometheus & OpenTelemetry** | Monitoring and observability support. |
| **Swagger Integration** | API documentation and testing UI. |
| **Database Migration** | Uses `migrate` tool to manage schema changes. |

---

## Pre-requisites

The Salary API requires these services before running the application:

- ScyllaDB  
- Redis  
- Migrate  
- Maven  

---

## Dependencies

### Build Time Dependencies  
| **Name** | **Description** |
|----------|------------------|
| Maven | Java build tool & dependency manager |
| JDK 17+ | Required for compiling and running the application |

### Run Time Dependencies  
| **Name** | **Version** | **Description** |
|----------|-------------|------------------|
| ScyllaDB | Latest | Primary datastore |
| Redis | Latest | Cache database |
| Migrate | Latest | Database migration tool |
| Java Runtime | 17+ | Required to execute the JAR |

### Other Dependencies  
| **Name** | **Description** |
|----------|------------------|
| Prometheus | Exposes monitoring metrics |
| OpenTelemetry | Observability and tracing |

---

## Important Ports

| **Port** | **Description** |
|----------|------------------|
| **8080** | Salary API service port |
| **9042** | ScyllaDB |
| **6379** | Redis |
| **80 / 443** | External package installation |

---

## Architecture

<img width="1760" height="760" alt="salary1" src="https://github.com/user-attachments/assets/8cf9fb2d-3375-48c0-9f15-5ef72158e5a0" />


---

## Dataflow Explanation

- Client sends salary data → **POST /api/v1/salary/create/record**
- Spring Boot controller receives request
- Redis cache optionally checked
- ScyllaDB queried or updated
- Redis cache updated/invalidated
- Response sent back to client
- Metrics sent to Prometheus/OpenTelemetry

---

## Installation Guide

Use the below link for step by step installation, to set up & run Salary API service.
https://github.com/Snaatak-Downtime-Rakshak/Documentation/tree/SCRUM-590-rajnish/OT-MS-Understanding/Application/Salary/POC

---

## Disaster Recovery

A proper disaster recovery plan ensures the Salary API can be restored quickly after unexpected failures such as data corruption, infrastructure failure, or accidental deletions.


| **Area**          | **Description**                          |
| ----------------- | ---------------------------------------- |
| Database Backups  | Use ScyllaDB snapshots for daily backups |
| Migration Backups | Keep migration history secure            |
| Cache Recovery    | Redis can rebuild cache from database    |


---


## High Availability

High availability ensures the Salary API remains operational with minimal downtime, even during failures or maintenance.

| **Area**                 | **Description**                                        |
| ------------------------ | ------------------------------------------------------ |
| API Redundancy           | Use multiple Salary API instances with load balancing. |
| ScyllaDB HA              | Multi-node Scylla cluster enhances reliability.        |
| Redis HA                 | Use Redis Cluster or replication.                      |
| Monitoring               | Prometheus-alerting + OpenTelemetry dashboards.        |
| Zero Downtime Deployment | Prefer rolling deployments/blue-green releases.        |

## Troubleshooting

| **Issue**                   | **Cause**                             | **Solution**                                     |
| --------------------------- | ------------------------------------- | ------------------------------------------------ |
| ScyllaDB Connection Failure | Wrong configuration or DB not running | Verify DB status and update `application.yml`    |
| Redis Unreachable           | Redis service is down                 | Start Redis: `sudo systemctl start redis-server` |
| Swagger Not Loading         | Incorrect port                        | Ensure service runs on port 8080                 |
| Migration Errors            | Incorrect DB credentials              | Fix `migration.json` and rerun migrations        |

---

## Contact Information
| Name              | Email Address                                    |
|-------------------|--------------------------------------------------|
| Abhishek           | abhishek.bisht.snaatak@mygurukulam.co            |

---

## References

| Topic                  | Link                                                                             |
| ---------------------- | -------------------------------------------------------------------------------- |
| Salary API Source      | ([Internal repository link as applicable](https://github.com/OT-MICROSERVICES/salary-api))     |
| ScyllaDB Documentation | [https://www.scylladb.com/docs/](https://www.scylladb.com/docs/)                 |
| Redis Documentation    | [https://redis.io/docs/](https://redis.io/docs/)                                 |
| Spring Boot Docs       | [https://spring.io/projects/spring-boot](https://spring.io/projects/spring-boot) |

---

