
1. IaaS Deployment
Steps for Deployment

1.1 Create Virtual Machines (VMs):
VM 1: Host the Flask web server and React UI.
VM 2: Host the Postgres database.
Use the following Azure VM configuration:
Operating System: Linux (Ubuntu 24.04)
Size: Standard B1s (1 vCPU, 1 GiB memory)
Public IP Address: 20.151.161.253
Network: Lab2_vnet/default

1.2 Set Up Networking:
Create a Virtual Network (Lab2_vnet) to ensure secure communication between components.
Configure firewall rules to allow HTTP/HTTPS traffic and restrict database access to internal traffic only.

1.3 Attach Persistent Storage:
Use Azure-managed disks for the database VM to store data reliably.

1.4 Configure Load Balancer:
Set up an Azure Load Balancer to route incoming requests to the web server VM for high availability.

1.5 Test Connectivity:
Verify that the Flask web server is accessible via the public IP address (20.151.161.253).

Architecture Diagram

 
            User Devices      
                 ↓
         Azure Load Balancer
       
                 ↓
        Flask & React Server 
            (Ubuntu VM)      
      
                 ↓
          Postgres Database  
             (Ubuntu VM)      
      

2. PaaS Deployment
Steps for Deployment

2.1 Deploy Web Application:
Use Azure App Service to host the Flask web server and React front end.
Configure the App Service to scale automatically based on traffic.

2.2 Set Up Managed Database:
Use Azure Database for PostgreSQL to handle database operations like scaling, backups, and updates.
Connect the App Service to the managed database via a secure connection string.

2.3 Enable Blob Storage:
Use Azure Blob Storage to store static assets such as images, CSS, and JavaScript files.

2.4 Monitor and Scale:
Leverage Azure’s built-in monitoring tools to track application performance and adjust resources dynamically.

2.5 Test Application:
Verify that the web application is accessible via the assigned App Service URL.

Architecture Diagram

       
            User Devices      
       
                  ↓
      
          Azure App Service    
         (Flask & React Front) 
       
                 ↓
       
         Azure Postgres DB   
       
                 ↓
      
         Azure Blob Storage   
       
