# Kubernetes WordPress & MySQL Multi-Container Infrastructure

A production-ready, local DevOps project demonstrating how to deploy a scalable, multi-container web application architecture on Kubernetes using standard manifests. 

This project provisions a classic 2-tier application infrastructure featuring a stateless WordPress frontend scaled for high availability, alongside a stateful, persistent MySQL database backend.

---

##  Architecture Overview

The infrastructure separates concerns across three core layers:

* **Compute Tier:** Deployments manage the desired state of the application containers. The WordPress container runs Apache/PHP, while the backend container runs the MySQL database engine.
* **Storage Tier:** Persistent Volume Claims (PVCs) dynamically request storage from the cluster to ensure that database records and media uploads survive container restarts.
* **Networking Tier:** Service objects provide static endpoints. WordPress safely communicates with the database using Kubernetes internal DNS (`mysql-service:3306`), while traffic is balanced across frontend application pods using built-in round-robin load balancing.

---

##  Project Structure

```text
my-k8s-project/
├── k8s/
│   ├── base/
│   │   └── secret.yaml       # Encrypted database credentials & root passwords
│   ├── mysql/
│   │   └── mysql.yaml        # Headless Service, PVC, & MySQL Deployment
│   └── wordpress/
│       └── wordpress.yaml    # NodePort Service, PVC, & WordPress Deployment (5 Replicas)
├── .gitignore                # Safeguard to prevent committing sensitive secrets
└── README.md                 # Project documentation