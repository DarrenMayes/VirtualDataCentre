# Hybrid Network Architecture

[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/) <a href="http://armviz.io/#/?load=https://raw.githubusercontent.com/DarrenMayes/HybridNetworkArchitecture/master/azuredeploy.json" target="_blank">
  <img src="http://armviz.io/visualizebutton.png"/>
</a>

Welcome to the Hybrid Network Architecture Azure Resource Manager template repository. This GitHub repo has been created to help promote the Security Architecture principles of "Secure By Design", "Compartmentalisation" and "Defense in Depth", whilst embracing the concept of "Infrastructure-as-Code" for automation, elasticity and repeatable deployment. It aims to achieve this by adopting a tailored Zero Trust Network Architecture pattern into an Azure Resource Manager Template which, at the click of a button can be deployed within a target subscription for Evaluation, Testing and eventually the Hosting of IaaS and PaaS Services. 

The template has been designed to benefit from the Microsoft recommend practice of deploying a Shared Services Virtual Network [HUB] which is peered to a Production or Test Virtual Network [SPOKE]. The Shared Services VNET contains all common Network Security components, needed for traffic analysis, inspection, management and response, such as a Centralised Layer 7 Firewall, Application Gateway, Web Application Firewall and Log Management. The design uses a multi-tiered network zone architecture to *Compartemtalise* services across functional boundaries, each of which are protected by a Network Security Group firewall at the Subnet Level to ensure *Defense in Depth*. 

The template is customisable and can be used to build and generate similar network patterns within an Azure Subscription and of course can be expanded to support your unique use cases. Naming conventions and IP schemas can be changed to better reflect your context and as such are not dependancies for success. 

*Please note that use of this template remains at the risk of the subscriber*. 

***Paramaters***

|Name                                   |Value              |Description                                                      |
|:---                                   |:---               |:---                                                             |
|'saType'                               |Standard_LRS       |Used to define the Storage Account Type                          |
|'aZFWRouteTables'                      |RT-TP-EU-AZFW      |Route Table for Internet  via Azure Firewall                     |
|'azUDRINT'                             |UDR-TP-EU-INT      |Internet 0.0.0.0/0 Route via Azure Firewall                      |
|'azUDRSS'                              |UDR-TP-EU-SS       |HUB 172.16.0.0/16 Route via Azure Firewall                       |                                     
|'azUDRSPOKE'                           |UDR-TP-EU-SPOKE    |SPOKE 10.102.0.0/16 Route via Azure Firewall                     |                                        
|'azvirtualNetwork1'                    |VNET-TP-EU-SS      |SHARED SERVICES *HUB* VIRTUAL NETWORK                            |
|'azvirtualNetwork2'                    |VNET-TP-EU-PRD     |PRODUCTION *SPOKE* VIRTUAL NETWORK                               |
|'resourceEULocation'                   |West Europe        |Location where Resources will be deployed                        |
|'azfirewallName'                       |AZFW-TP-EU-SS      |Name of the Azure Firewall deployed within SHARED SERVICES *HUB* |
|'azureFirewallSubnetAddressPrefix'     |172.16.254.0/26    |Private Subnet Used by the Azure Firewall                        |
|'numberOfPublicIPAddresses'            |1                  |Count of Public IP Addressess used by Azure Firewall             |
|'publicIPNamePrefix'                   |PIP-TP-EU-AZFW     |Name of the Public IP Addressess used by Azure Firewall          |  
|'availabilityZones'                    |"1", "2", "3"      |Used to mitigate risk of Azure Datacenter Failure                |                                       
|'nsgMGMTSS'                            |NSG-MGMT-EU-SS     |Name of Shared Services Management Subnet NSG                    |                                      
|'nsgSPWEB'                             |NSG-WEB-EU-PRD     |Name of Production Web Subnet NSG                                | 
|'nsgSPAPP'                             |NSG-APP-EU-PRD     |Name of Production App Subnet NSG                                |                               
|'nsgSPDB'                              |NSG-DB-EU-PRD      |Name of Production DB Subnet NSG                                 |                                
|'nsgSPID'                              |NSG-ID-EU-PRD      |Name of Production DB Subnet NSG                                 |                               


**Change Management**
- [x] Update template to include Azure Firewall for Spoke Virtual Network and introduce base rules
- [x] Introduce VNET Peering between Shared Services HUB and Production Spoke Virtual Networks
- [x] Create UDR and associate with Production Spoke Subnets to allow inspection in Shared Services HUB
- [x] Create and associate Network Security Group to filter traffic at subnet level of Spoke Virtual Network
- [ ] Include Service Endpoints for Microsoft.Storage to integrate sensitive accounts with VNET
- [ ] Create Storage Account and integrate Diagnostic Logs for Azure Firewall for forensics and analysis
- [ ] Modify the template to include Virtual Network Gateway in readiness for S2S VPN
- [ ] Incorporate an Application Gateway with Web Application Firewall Functionality closest to Web Subnet
- [ ] Create Test VM to validate approved traffic flows from Shared Services HUB to Production Spoke

