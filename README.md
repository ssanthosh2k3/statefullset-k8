# E2E Kubernetes Database Service Access Guide

This guide provides detailed instructions to access the database service hosted on your Kubernetes cluster. The database can be accessed internally using either SSL VPN or via a jump server.

---

## **Table of Contents**

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [Access Methods](#access-methods)
    - [Method 1: Using SSL VPN](#method-1-using-ssl-vpn)
    - [Method 2: Using a Jump Server](#method-2-using-a-jump-server)
4. [Example NodePort YAML Configuration](#example-nodeport-yaml-configuration)
5. [Troubleshooting](#troubleshooting)
6. [License](#license)

---

## **Overview**

This project demonstrates how to securely access a Kubernetes database service hosted in an E2E Kubernetes cluster. Two methods are provided for internal access:
- **Method 1**: Using an SSL VPN.
- **Method 2**: Using a jump server for GUI-based access.

---

## **Prerequisites**

Before accessing the database, ensure the following:
1. A Kubernetes cluster is set up in the E2E environment.
2. The database pods are deployed, and a NodePort service is configured.
3. Access to the same VPC as the Kubernetes cluster.
4. Required tools installed on your local or jump server:
   - `kubectl`
   - Database client (e.g., MongoDB Compass)

---

## **Access Methods**

### **Method 1: Using SSL VPN**

#### Step 1: Create a Firewall in the Same VPC
- Create a firewall under the same VPC as the Kubernetes cluster.

#### Step 2: Log in to the Firewall
- Use your email credentials to log in to the firewall.

#### Step 3: Configure SSL VPN
- Follow the [SSL VPN Configuration Guide](https://docs.google.com/document/d/1ja7qRqF462CqG-V5GSnTSpn7HxjJLJXVxPz2pgKGA/edit?tab=t.0).

#### Step 4: Set Up a NodePort Service
- Create a NodePort service to expose your database pods.

#### Step 5: Connect to the SSL VPN
- Connect to the SSL VPN from your local machine and verify connectivity by pinging Kubernetes worker nodes.

#### Step 6: Access the Database
- Use any worker node's VPC IP and the NodePort to connect via a database client.

---

### **Method 2: Using a Jump Server**

#### Step 1: Set Up a Jump Server
- Create a jump server under the same VPC as the Kubernetes cluster.

#### Step 2: Configure XRDP for GUI Access
- Install and configure XRDP to enable GUI access on the jump server.

#### Step 3: Set Up a NodePort Service
- Create a NodePort service for your database pods.

#### Step 4: Install a MongoDB Client Tool
- Install a MongoDB client tool on the jump server.
- Use the worker node's IP and NodePort to connect to the database.

---

## **Example NodePort YAML Configuration**

Use the following YAML configuration to create a NodePort service for your database pods:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: db-service
spec:
  type: NodePort
  ports:
    - port: 27017
      targetPort: 27017
      nodePort: 30017
  selector:
    app: database
