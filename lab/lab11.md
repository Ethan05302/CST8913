# MigrationPlan.md

## 1. Discovery and Tooling Setup

Tailwind should use the Azure Migrate appliance for discovery since it’s agentless and works well with their Ubuntu servers—no need to install stuff on each machine. Just set it up on a spare box in their data center and let it scan everything.

We need to collect: the Ubuntu OS version and kernel details, a software list (NGINX, Node.js, PostgreSQL, Redis, HAProxy) with versions, hardware specs like CPU, RAM, and disk size, network info (IPs, ports, firewall rules), and some basic dependency data to see how the servers talk to each other.

For credentials, I’d stash SSH keys in Azure Key Vault to keep them secure and limit who can grab them. Azure Migrate only needs read-only access, so I’d set that up with Azure’s role controls. On the servers, I’d create a dedicated user with just enough permissions—no root—to keep things tight.

---

## 2. Assessment Planning

In Azure Migrate, I’d configure it to use 30 days of performance history to catch peak loads from patient bookings. For sizing, I’d pick “as-is” to match their current setup, then add a 1.2x comfort factor so it’s ready for busier days.

Target region would be East US—close to users, low latency. Compute-wise, I’d go with Azure VMs (D2s v3) for NGINX and Node.js since they balance cost and power. Storage would be Premium SSD for PostgreSQL and Redis for speed, and Standard HDD for backups to save money.

To validate, I’d show the Azure Migrate report to Tailwind’s tech crew and app owners, checking if the VM sizes and costs fit their 99.9% uptime need. I’d also run a quick test in Azure with a small setup to make sure it holds up and tweak if they say it’s off.

---

## 3. Dependency Analysis and Optimization

I’d use Azure Migrate’s agentless dependency mapping to track how NGINX connects to Node.js, and how those hit PostgreSQL and Redis. It pulls network traffic data without touching the servers, which is perfect here.

To clean it up, I’d filter out system junk like Ubuntu’s cron or logging processes that don’t matter to the app—just keep the real app-to-app links clear. 

Key metrics are: criticality (database and backend can’t fail), user base (how many patients book daily), SLA (99.9% uptime, under 2 hours downtime), and backups (daily, keep 7 days). That’s what drives the plan.

---

## 4. Server Grouping and Migration Waves

Group the servers like this:  
- Frontend: 2 NGINX servers.  
- Backend: 2 Node.js servers.  
- Database: 1 PostgreSQL server.  
- Cache: 1 Redis instance.  
- Load balancer + backup: HAProxy and the Linux backup.

Wave 1 is Redis and the backup system—easy, low stakes, tests the process. Wave 2 is PostgreSQL since it needs data copied early to cut downtime. Wave 3 is Node.js, NGINX, and the load balancer together—they’re tight-knit, so they move as a unit.

Precautions: copy firewall rules to Azure’s network security groups, swap HAProxy for Azure Load Balancer and test it, and either lock in static IPs or update DNS fast so nothing breaks.

---

## 5. Migration Plan Documentation

Here’s the plan:  
1. **Prep**: Use Azure Site Recovery to replicate PostgreSQL to Azure Database for PostgreSQL ahead of time. Sync Redis to Azure Cache for Redis. App owners test the current system.  
2. **Setup**: Deploy D2s v3 VMs for NGINX and Node.js. Set up Azure Load Balancer to replace HAProxy with health checks. Move backups to Azure Blob Storage with daily runs.  
3. **Migrate**: Stop PostgreSQL replication, switch to Azure’s version (under 30 mins downtime). Move NGINX configs and Node.js code to VMs.  
4. **DNS**: Update DNS to point to Azure Load Balancer’s IP. Test connectivity.  
5. **Validate**: App owners check booking works. Confirm backups ran with latest data.  

App owners test pre-migration to spot issues, then validate post-migration to ensure patients see no difference. Downtime stays under 2 hours with the pre-replicated data.

---
