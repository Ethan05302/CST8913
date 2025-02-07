# High-Level Design (HLD) for Multi-Region Deployment with Load Balancing

## 1. Solution Architecture Diagram
The target architecture consists of two main components:
- **WebServerVM** (frontend server hosting static content)
- **SQLVM** (backend SQL database)

Both components are replicated across two cloud regions to ensure high availability. A **Global Load Balancer** distributes incoming traffic between regions, and each region has a **Local Load Balancer** to handle internal traffic distribution. The database is configured with **active-passive replication** and automatic failover in case of a regional outage.

### **Architecture Diagram**
The following diagram illustrates the multi-region deployment with load balancing and failover mechanisms:

![output (3)](https://github.com/user-attachments/assets/881c08ca-4bf4-49a1-8563-ca991db7b76a)


### **Key Components**
- **Global Load Balancer**: Routes user requests to the healthiest region.
- **Region Load Balancers**: Manage internal traffic within each region.
- **WebServerVM**: Replicated frontend servers to ensure high availability.
- **SQLVM Databases**: Primary and secondary instances with automatic failover.
- **Database Replication & Sync**: Ensures data consistency across regions.
- **Failover & DNS Routing**: Minimizes downtime in case of failures.
- **Monitoring & Logging**: AWS CloudWatch and Security Hub track system health.

## 2. Target Architecture Description
The architecture ensures high availability and redundancy through:
- **Multi-Region Deployment**: WebServerVM and SQLVM are deployed in two cloud regions.
- **Global Load Balancer**: Routes user requests to the healthiest region based on availability.
- **Local Load Balancers**: Handle load distribution within each region.
- **Database Replication & Failover**: SQLVM follows an active-passive setup with automatic failover to the secondary region if the primary fails.
- **Downtime Management**: Automated failover mechanisms ensure downtime does not exceed the 6-hour limit.

## 3. Migration Steps

### Step 1: Virtual Machine Replication Across Regions
- Deploy WebServerVM and SQLVM in the primary region.
- Create identical instances in the secondary region.
- Configure data synchronization between SQLVM instances using **SQL replication**.

### Step 2: Configure Load Balancers
- Deploy a **Global Load Balancer** to distribute traffic between regions.
- Set up **Local Load Balancers** in each region for internal traffic management.
- Define **health checks** to ensure requests are routed to healthy instances.

### Step 3: Implement Database Replication & Failover
- Configure **asynchronous replication** between the primary and secondary SQLVM.
- Set up **automated failover** to promote the secondary SQLVM if the primary fails.
- Implement **DNS failover** to reroute traffic in case of regional downtime.
