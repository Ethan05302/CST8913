# Modernizing a Legacy Application to a Cloud-Native Architecture in Microsoft Azure

## 1. Architecture Diagrams

### **Before Refactoring:**
The original architecture consists of a monolithic web application running on a single Windows Server 2019 VM in Azure. It includes:

```
+---------------------+
| User Requests      |
+---------------------+
        |
        v
+---------------------+
| Windows Server VM  |
| - Web Framework    |
| - IIS Hosting      |
| - SQL Server       |
| - Task Scheduler   |
+---------------------+
        |
        v
+---------------------+
| Local Disk Storage |
+---------------------+
```

### **After Refactoring:**
The refactored architecture leverages Azure cloud-native services, including:

```
+---------------------+
| User Requests      |
+---------------------+
        |
        v
+---------------------+
| Azure App Service  |
+---------------------+
        |
        v
+---------------------+
| Azure SQL Database |
+---------------------+
        |
        v
+---------------------+
| Azure Blob Storage |
+---------------------+
        |
        v
+---------------------+
| Azure Functions    |
+---------------------+
```

## 2. Migration Process

### **Step 1: Assess Existing Architecture**
- Identify monolithic components and dependencies.
- Analyze database structure and connections.
- Review background task handling and static file storage.

### **Step 2: Plan Refactoring Strategy**
- Define service boundaries and select appropriate Azure services.
- Establish an authentication and authorization strategy (e.g., Azure AD).

### **Step 3: Execute Migration**
1. **Deploy Web Application to Azure App Service**
   - Set up an App Service Plan.
   - Deploy application code via CI/CD.
2. **Migrate Database to Azure SQL Database**
   - Use Azure Database Migration Service.
   - Configure application connection strings.
3. **Convert Background Jobs to Azure Functions**
   - Identify scheduled tasks and refactor them into serverless functions.
   - Deploy and configure function triggers.
4. **Move Static Files and Logs to Azure Blob Storage**
   - Create a storage account and blob containers.
   - Update application logic to integrate with Blob Storage.

### **Step 4: Optimize and Validate**
- **Enable Auto-Scaling** for the web application.
- **Set Up Monitoring & Logging** using Azure Monitor and Application Insights.
- **Conduct Performance & Reliability Testing** (load testing, failover testing, etc.).

