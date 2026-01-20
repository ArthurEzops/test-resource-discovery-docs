# Multi-Cloud Infrastructure - Test Resources
---

## 🌩️ AWS Resources (us-east-1)

### Kubernetes

- **EKS Cluster:** production-ace-eks
  - Region: us-east-1
  - Account: 975635808270
  - Namespace: prod
  - Purpose: Production workloads for ACE platform

### Databases

- **RDS PostgreSQL:** production-env-db
  - Endpoint: production-env-db.cxrmz3cohr4b.us-east-1.rds.amazonaws.com
  - Port: 5432
  - Engine: PostgreSQL 14
  - Databases: llmdatabase, configuration, docs, schedule

### Storage

- **S3 Bucket:** zng-ezops-br-ace
  - Purpose: Database dumps, backups, artifacts
  - Prefix for dumps: db-dumps/prod

- **EFS Volume:** fs-058b921d6c09815cf
  - Purpose: Persistent storage for Kubernetes pods
  - Mount path: /mnt/efs

### Container Registry

- **ECR Repository:** 975635808270.dkr.ecr.us-east-1.amazonaws.com/ace/llm
  - Purpose: Docker images for LLM API
  - Tags: prod-*, dev-*

---

## ☁️ GCP Resources (us-central1)

### Kubernetes

- **GKE Cluster:** analytics-gke-cluster
  - Region: us-central1
  - Zone: us-central1-a
  - Node pool: 5 nodes (n1-standard-4)
  - Purpose: Analytics microservices

### Databases

- **Cloud SQL PostgreSQL:** analytics-cloudsql-db
  - Region: us-central1
  - Instance: db-n1-standard-2
  - Database: analytics_prod
  - Connection: via Cloud SQL Proxy

- **Cloud SQL MySQL:** staging-mysql-instance
  - Region: us-central1
  - Purpose: Staging environment for testing

- **BigQuery Dataset:** ezops_analytics_prod
  - Location: US
  - Tables: user_events, system_metrics, llm_usage
  - Purpose: Data warehouse for analytics

### Storage

- **Cloud Storage Bucket:** ezops-analytics-backups
  - Location: US
  - Storage class: STANDARD
  - Purpose: Analytics data backups

- **Cloud Storage Bucket:** ezops-ml-models
  - Purpose: ML model storage and versioning

### Compute

- **Compute Engine VM:** analytics-processing-vm
  - Zone: us-central1-a
  - Machine type: n1-highmem-8
  - Purpose: Heavy data processing jobs

- **Cloud Run Service:** api-analytics-service
  - Region: us-central1
  - Purpose: Analytics API endpoints

---

## 🔷 Azure Resources (East US)

### Kubernetes

- **AKS Cluster:** dr-aks-cluster-prod
  - Location: East US
  - Resource Group: ezops-dr-prod-rg
  - Node count: 3 (Standard_D4s_v3)
  - Purpose: DR environment, can be activated quickly

- **AKS Cluster:** dr-aks-staging
  - Location: East US
  - Resource Group: ezops-dr-staging-rg
  - Purpose: Staging environment

### Databases

- **Azure SQL Database:** backup-sql-prod
  - Server: ezops-backup-sqlserver.database.windows.net
  - Location: East US
  - Tier: Standard S3
  - Purpose: Replicated production data

- **Cosmos DB:** ezops-dr-cosmosdb
  - Location: East US (with geo-replication)
  - API: SQL API
  - Purpose: NoSQL backup and DR

### Storage

- **Azure Storage Account:** ezopsdrbackupstorage
  - Location: East US
  - Replication: GRS (Geo-Redundant Storage)
  - Container: dr-backups

- **Azure Storage Account:** ezopsdrlogs
  - Purpose: DR environment logs
  - Tier: Cool (cost-optimized for infrequent access)

### Networking

- **Azure Load Balancer:** dr-lb-prod
  - Type: Standard
  - Purpose: Load balancing for AKS ingress

- **Application Gateway:** dr-appgw-001
  - SKU: WAF_v2
  - Purpose: Web application firewall and routing

### Compute

- **Azure Functions:** dr-notification-func
  - Region: East US
  - Purpose: Send alerts during DR activation

- **Virtual Machine:** dr-jumpbox-vm
  - Size: Standard_B2s
  - Purpose: Jump box for secure access to DR environment

---

## 📊 Expected Resources

- **Total:** ~20 recursos
- **AWS:** 5 recursos (EKS, RDS, S3, EFS, ECR)
- **GCP:** 8 recursos (GKE, 3x DB, 2x Storage, VM, Cloud Run)
- **Azure:** 7 recursos (2x AKS, 2x DB, 2x Storage, LB, Functions, VM)

---

## ✅ Validation

Após rodar o `/discovery` endpoint, você deve ver:

1. **Providers detectados:** aws, gcp, azure
2. **Resource types:** kubernetes, database, storage, compute, network
3. **Resource subtypes:** eks, gke, aks, rds, cloudsql, s3, gcs, etc.
4. **Provider resource IDs:** ARNs, GCP paths, Azure resource IDs
5. **Metadata:** Regiões, contas, namespaces, etc.

---

**Última atualização:** 2026-01-20

