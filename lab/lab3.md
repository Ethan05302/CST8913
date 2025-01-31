# Cloud Migration Lab Report

## On-Premises Architecture Design  

### Architecture Diagram  

         +------------------+        +------------------+        +----------------------+
         |  Web Application | ----> |   SQL Database   | ----> |  Local File System   |
         +------------------+        +------------------+        +----------------------+
                  |                           |                            |
                  v                           v                            v
         +------------------+        +------------------+        +----------------------+
         |    End Users     | <----  | Firewall/Router  | ----> |   Email Service     |
         +------------------+        +------------------+        +----------------------+

### Architecture Summary
The on-premises architecture consists of tightly coupled components that work together to handle web application traffic, data storage, and user notifications. While functional, this architecture faces challenges such as scalability, maintenance overhead, and limited disaster recovery options, making it a candidate for cloud migration.

## Component Descriptions  

### Web Application  
- **Type**: Monolithic application hosted on physical servers.  
- **Dependencies**:  
  - Communicates with the SQL database for transaction processing.  
  - Stores static files in the local file system.  
  - Triggers email notifications via the on-premises email service.  
- **Challenges**: Limited scalability and reliance on physical infrastructure.

### SQL Database  
- **Role**: Manages inventory, customer data, and transactions.  
- **Hosting**: Dedicated physical server with nightly backups.  
- **Challenges**: High operational costs and lack of real-time failover support.

### Local File Storage  
- **Functionality**: Stores static assets (images, documents) in a directory-based structure.  
- **Path**: `/var/www/storage` (integrated with the web application).  
- **Challenges**: No redundancy and limited storage capacity.  

### Networking  
- **Components**:  
  - Firewalls restrict external access to ports 80  and 443.  
  - Routers manage internal traffic between servers and end users.  
- **Challenges**: Potential bottlenecks during peak usage.  

### Email Service  
- **Setup**: Self-hosted Postfix server for client notifications.  
- **Integration**: Called by the web application via SMTP.  
- **Challenges**: Limited scalability and risk of email delivery issues.

## Dependencies  
- Web app → SQL Database (read/write operations).  
- Web app → Local File Storage (file uploads/downloads).  
- Web app → Email Service (notification triggers).  
- Firewalls secure all inbound/outbound traffic.  

---

# Cloud Migration Plan

## Migration Strategies

### Web Application  
- **Current:** Monolithic web app on physical servers.  
- **Target:** PaaS or IaaS.  
- **Strategy:** Lift and shift to IaaS or refactor for PaaS.  

### Database  
- **Current:** SQL Server on-premises.  
- **Target:** PaaS (e.g., AWS RDS) or IaaS.  
- **Strategy:** Rehost to IaaS or migrate to managed PaaS.  

### File Storage  
- **Current:** Local file system.  
- **Target:** Cloud storage (e.g., AWS S3).  
- **Strategy:** Direct file transfer to cloud storage.  

### Networking  
- **Current:** On-premises routers/firewalls.  
- **Target:** Cloud networking (e.g., AWS VPC).  
- **Strategy:** Set up VPN or Direct Connect.  

### Email Service  
- **Current:** Self-hosted email service.  
- **Target:** SaaS or PaaS.  
- **Strategy:** Switch to cloud-based email services.  

## Migration Steps
1. **Assessment**: Conduct a detailed analysis of existing systems, including dependencies, performance metrics, and potential risks.  
2. **Cloud Environment Setup**: Configure the target cloud platform, ensuring proper networking and security controls.  
3. **Database Migration**: Use tools like AWS Database Migration Service to rehost or replatform the database.  
4. **File Storage Migration**: Transfer static files to cloud storage using scripts or migration tools.  
5. **Application Deployment**: Deploy the web application to the target platform and test its functionality.  
6. **Validation and Optimization**: Test end-to-end workflows, monitor performance, and optimize configurations.  
7. **Go Live**: Transition users to the cloud environment and decommission on-premises infrastructure.

