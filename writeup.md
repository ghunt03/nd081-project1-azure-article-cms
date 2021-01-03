# Write-up Template

## Analyze, choose, and justify the appropriate resource option for deploying the app.

*For **both** a VM or App Service solution for the CMS app:*
- *Analyze costs, scalability, availability, and workflow*
- *Choose the appropriate solution (VM or App Service) for deploying the app*
- *Justify your choice*




### Costs 
#### General
The pricing for both Azure Virtual Machines and Azure App Services completely depends on the resource requirements of the application. 

Pricing can be determined using the Azure Pricing Calculator

Depending on the configuration of the application we would also need to consider:
- Azure Storage
- Azure SQL Database
- SSL Certifcates
- Domain name / hosting

#### Azure Virtual Machine
At the time of writing a virtual machine capable of running with the following resources:
- 1 Core
- 1.75GB RAM
- 40GB storage
- Running Linux

Would cost USD 0.031 / hour


#### Azure App Services
At the time of writing a virtual machine capable of running with the following resources:
- 1 Core
- 1.75GB RAM
- 10GB storage

Would cost USD 0.018 / hour


### Availabilty
#### Azure Virtual Machine
Running a virtual machine provides more control over the when the server is running. There are options to only have the server running when needed, for example if the application is only needed during specific events or hours of the day it could be shutdown to reduce the running costs of the application.

#### Azure App Services
Running the app in Azure App Services limits the options here, the application will incur costs even when not in use as there are no options to shutdown the application only to remove it.


### Scalability
#### Azure Virtual Machine
Azure Virtual Machines provide a maximum limit of:
- 5700GB RAM
- 416 Cores
- 8192GB Storage

We are also provided the option of scaling sets which allows us to cluster multiple servers together, however this would require the application to be developed in such a way to support this.

On this basis the scalability of the application shouldn't be an issue. 

#### Azure App Services
Azure App Services has a maximum limit of
- 32GB RAM
- 8 Cores
- 250 GB Storage (shouldn't be an issue as the bulk of the storage is in Azure SQL Database and an Azure Storage Account)

Providing the app doesn't require more than this it should be sufficient.

### Workflow
#### Azure Virtual Machine
To setup a Virtual Machine on Azure more work is required upfront such as ensuring the right operating system is selected, right resources and security.

Once the VM is up and running additional functionality is needed to ensure the application is running correctly and the operating system and packages are up to date. In the case of this application we would need to install and configure NGINX if we were running on a linux server.


#### Azure App Services
Setting up the environment to run the application in Azure App Services is generally a lot easier than setting up a VM at least intially as there is no need to worry about the Operating System level.

Deploying new versions of the app is generally a lot simpler on Azure App Services. The app can be deployed and updated through Github Actions and as new versions are committed to the main repository the code can be automatically updated. This allows us to take a CI/CD approach to releasing new versions. We can also setup automated testing as part of the deployment process



### Recommendation
Given the initial scale and requirements for this particular application I recommend the use of Azure App Services. 

However if the scale needed to be ramped up or if the client required additional security such as dedicated servers, we could then look at migrating the application over to an Azure Virtual Machine. This would provide increased security and more control over the server at the operating system level. 

For this to occur we would need to look at the deployment methods and setting up git on the server to ensure it is running the latest code.



