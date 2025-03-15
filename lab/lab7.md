# Azure Cost Management Lab Report

---

## 1. Cost Estimate (Azure Pricing Calculator)

### Service Breakdown
| Service Category | Service Type         | Description                                                                                     | Estimated Monthly Cost (USD) |
|------------------|---------------------|-------------------------------------------------------------------------------------------------|-----------------------------:|
| Compute          | Virtual Machines    | 1 B2s (2 Cores, 4 GB RAM) x 730 Hours (Pay as you go), Windows (License included), OS Only; 1 managed disk – S6; Inter Region transfer type, 5 GB outbound data transfer from East US to East Asia | $39.216                     |
| Compute          | Virtual Machines    | 1 D2s v3 (2 vCPUs, 8 GB RAM) x 730 Hours (Pay as you go), Windows (License included), OS Only; 1 managed disk – P10; Inter Region transfer type, 5 GB outbound data transfer from East US to East Asia | $156.95                     |
| Databases        | Azure SQL Database  | Single Database, vCore, General Purpose, Provisioned, Standard-series (Gen 5), Primary or Geo replica Disaster Recovery, Locally Redundant, 1 - 2 vCore Database(s) x 730 Hours, 128 GB Storage, SQL License (Pay as you go), RA-GRS Backup Storage Redundancy, 0 GB Point-In-Time Restore, 0 x 5 GB Long Term Retention | $387.32318                  |
| Networking       | Bandwidth           | Inter Region transfer type, 200 GB outbound data transfer from West US to East Asia              | $9.75                       |

### Total Estimated Monthly Cost
- **Total**: **$593.23918 USD**

### Notes
- All prices are in United States – Dollar ($) USD.
- This is a summary estimate, not a quote.
- Estimate created on **March 15, 2025, 2:26:39 AM UTC**.

---

## 2. Cost Reports (Azure Cost Analysis)

### Cost Breakdown by Resource Type
| Resource Type                     | Cost (USD)       |
|-----------------------------------|-----------------:|
| microsoft.datafactory/factories   | $0.000243        |
| microsoft.compute/disks           | $0.018056        |
| microsoft.compute/virtualmachines | $0.032653        |
| microsoft.network/bastionhosts    | $0.226206        |
| microsoft.network/privatednszones | $0.000610        |
| microsoft.network/privateendpoints| $0.017067        |
| microsoft.network/publicipaddresses| $0.010617       |
| microsoft.storage/storageaccounts | $0.000003        |
| microsoft.insights/actiongroups   | $0.000000        |
| **Total**                         | **$0.306457**    |

---

## 3. Budgets and Alerts (Azure Portal)

### Budget Configuration
- **Budget Name**: Monthly-Budget-50
- **Scope**: Subscription
- **Amount**: $50
- **Reset Period**: Monthly

### Alert Settings
- **50% Threshold**: $25
- **90% Threshold**: $45

### Screenshots
1. **Budget Configuration**:
2. **Alert Settings**:
  
<img width="624" alt="budget-alert" src="https://github.com/user-attachments/assets/fa7bcdb6-5109-43cc-849e-a9ffa7a5466c" />

---

## 4. Tagging Strategy

### Tags Applied
- **Environment: Test**  
  Identifies resources used for testing purposes.
- **Department: IT**  
  Assigns ownership to the IT team for cost tracking.

### Purpose of Tags
- **Environment**: Helps differentiate between production, development, and testing resources.
- **Department**: Tracks resource ownership and cost allocation by department.

### Tagging Implementation
1. **Login to Azure Portal**:
   - Navigate to the desired resource group or resource.
2. **Add Tags**:
   - Go to the **Tags** section.
   - Add the following tags:
     - **Name**: `Environment` → **Value**: `Test`
     - **Name**: `Department` → **Value**: `IT`
   - Click **Apply** to save the tags.
3. **Verify Tags**:
   - Ensure the tags are correctly applied to the resources.

---

### **Notes**
- Tags are essential for organizing resources and managing costs effectively.
- Use consistent naming conventions for tags across all resources.
