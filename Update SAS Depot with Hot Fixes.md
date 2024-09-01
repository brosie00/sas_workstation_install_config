# Introduction  
SAS releases hotfixes to address security needs.  Unlike Windows or Microsoft Office, there is no monolithic installer or updater. We go back to the original SAS Depot and run 

# Overview 
- Inventory the SAS Installation and produce DeploymentRegistry.txt
- Export the DeploymentRegistry.txt file to a non-IRS workstation with direct Internet access
- Use a sas tool ( SASHFADD ) to process the inventory and produce a list of needed hotfixes
- Use a script to download the hotfixes
- Move the hotfixes to an IRS workstation
- Install hotfixes
- 

