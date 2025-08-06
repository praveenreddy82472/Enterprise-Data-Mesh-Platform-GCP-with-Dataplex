# Enterprise Data Mesh Platform on Google Cloud with Dataplex

## Overview

In today's data-driven world, organizations often manage massive volumes of data across multiple business domains—each with its own unique requirements and challenges. Imagine a large enterprise with separate teams for Airlines, Hotels, and Ride-sharing services, each generating valuable data every second. But how do you bring this data together in a way that respects each domain’s autonomy, ensures strong security, and enables centralized governance and discovery?

# This project answers that question.

## The Problem

Traditionally, data from various domains ends up siloed in disconnected systems. This leads to:

- Security risks from inconsistent access control  
- Complex governance and compliance challenges  
- Difficulties in discovering and cataloging data assets  
- Data duplication and inefficient pipelines  
- Lack of visibility into data lineage and quality  

Enterprises need a centralized yet flexible platform—one that allows domain teams to manage their own data while providing an umbrella for unified governance, security, and metadata management.

## The Vision

Build a centralized Enterprise Data Mesh using Google Cloud Platform’s Dataplex, BigQuery, and Cloud Storage to:

- Manage data per domain (Airlines, Hotels, Ride-sharing) with clear boundaries  
- Store raw data securely and immutably in Cloud Storage (Raw Zone)  
- Maintain curated, analytics-ready data in BigQuery (Curated Zone)  
- Enforce customer-managed encryption keys (CMEK) to meet stringent security requirements  
- Use Dataplex as the single pane of glass to register data assets, manage metadata, enforce access policies, and perform data quality checks  
- Enable self-service discovery, monitoring, and governance for data consumers and governance teams alike  

# Architecture Overview

```plaintext
+---------------------------------------------------------------+
|                      Enterprise Data Mesh                     |
|                                                               |
|  +----------------+     +----------------+     +------------+ |
|  |                |     |                |     |            | |
|  |  Domain:       |     |  Domain:       |     |  Domain:   | |
|  |  Airlines      |     |  Hotels        |     |  Ride-share| |
|  |                |     |                |     |            | |
|  +-------+--------+     +--------+-------+     +-----+------+ |
|          |                       |                     |      |
|  Raw Zone: GCS Buckets   Raw Zone: GCS Buckets  Raw Zone: GCS |
|  (encrypted with CMEK)   (encrypted with CMEK)   (encrypted)  |
|          |                       |                     |      |
|          v                       v                     v      |
| +----------------+      +----------------+    +----------------+|
| | Curated Zone:  |      | Curated Zone:  |    | Curated Zone:   ||
| | BigQuery Datasets|    | BigQuery Datasets|  | BigQuery Datasets||
| |  (CMEK enabled)  |    |  (CMEK enabled) |   |  (CMEK enabled)  ||
| +----------------+      +----------------+    +----------------+|
|          |                       |                     |      |
|          +------------+----------+----------+----------+      |
|                       |                     |                 |
|             +-------------------------------+                 |
|             |        Dataplex Central Lake  |                 |
|             |  - Manages lakes and zones    |                 |
|             |  - Registers GCS and BigQuery |                 |
|             |  - Metadata, lineage, policy |                  |
|             +-------------------------------+                 |
|                       |                                       |
|                +----------------+                             |
|                | Access Control |  <-- IAM Roles assigned per |
|                | & Governance   |      domain/team            |
|                +----------------+                             |
|                       |                                       |
|               +------------------+                            |
|               |  Data Catalog    |                            |
|               | (Metadata Tags,  |                            |
|               |  Data Lineage)   |                            |
|               +------------------+                            |
|                                                               |
+---------------------------------------------------------------+





## Why This Approach?

- **Decouples domain ownership and governance:** Each domain manages their own data lifecycle within their lakes and zones, reducing bottlenecks.  
- **Centralizes metadata and policies:** Dataplex provides a unified catalog and governance layer so governance teams can oversee data security and compliance.  
- **Improves security posture:** With CMEK encryption, fine-grained IAM permissions, and audit visibility, the data is protected end-to-end.  
- **Simplifies data discovery and quality:** Automated profiling and quality scans help maintain trust in the data.  
- **Future-proof and scalable:** Designed to evolve with more domains, data sources, and analytic needs.  

## What You’ll See in This Project

- Creation of domain-specific Cloud Storage buckets for raw data ingestion  
- Use of Customer-Managed Encryption Keys (CMEK) to secure data at rest  
- Creation of BigQuery datasets as curated zones for analytics  
- Setup of Dataplex lakes and zones, registering raw and curated assets  
- Application of IAM roles and permissions to simulate domain-level access control  
- Examples of data profiling and quality scans within Dataplex  
- Instructions to visualize data with tools like Looker Studio  

## Advantages of This Architecture

- Domain autonomy + centralized governance: Balances agility and control  
- End-to-end security: CMEK encryption, IAM policies, and audit trails  
- Simplified operations: Manage data assets and metadata centrally  
- Improved data quality and trust: Automated scans surface issues early  
- Scalability: Add more domains or lakes easily without disruption  

## Who Is This For?

- Data engineers and architects looking to build scalable, secure data platforms  
- Organizations transitioning to data mesh or enterprise data lakes  
- Teams aiming to enforce strong governance without sacrificing domain agility  
- Anyone curious about how Google Cloud’s Dataplex and CMEK can elevate data management  

## How to Use This Repository

Explore the step-by-step instructions to:

- Set up your Google Cloud environment  
- Create and encrypt your storage buckets and BigQuery datasets  
- Configure Dataplex lakes, zones, and assets  
- Assign access controls to simulate domain-specific permissions  
- Load, profile, and curate data  
- Visualize insights using Looker Studio or other BI tools  

# Final Thoughts

This project is not just about technology—it’s about solving a real business problem: how to unify diverse data domains securely and efficiently while empowering each team to own their data. By leveraging Google Cloud’s powerful data management services, we create a platform that is both flexible and governed, simple yet powerful, and ready to scale with business needs.
