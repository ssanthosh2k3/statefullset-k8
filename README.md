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

---

## **Access Methods**

### **Method 1: Using SSL VPN**

1. **Create a Firewall in the Same VPC as the Kubernetes Cluster**  
   Ensure that the firewall is created under the same VPC used to create your Kubernetes cluster.

2. **Log in to the Firewall**  
   Open the FortiGate firewall dashboard using your email credentials.  
   ![FortiGate Dashboard](images/forti-dash.png)

3. **Configure SSL VPN**  
   Follow the provided [documentation](https://docs.google.com/document/d/1ja7qRqF462CqG-V5GSnTSpn7HxjJLJXVxPz2pgKGA/edit?tab=t.0) to configure SSL VPN for the firewall.

4. **Set Up a NodePort Service for Database Pods**  
   Create a NodePort service for your database pods, deployment, or StatefulSet.

5. **Verify the Service and Pods**  
   Use the following commands to check the status:  
   ```bash
   kubectl get pods
   kubectl get svc
