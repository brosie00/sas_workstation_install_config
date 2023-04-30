
# Table of Contents
- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
- [Use of this Document and Git Repo](#use-of-this-document-and-git-repo)
- [Remove Old SAS Client Install](#remove-old-sas-client-install)
- [Installation](#installation)
- [Common Installation Issues](#common-installation-issues)

What the project does
Why the project is useful
How users can get started with the project
Where users can get help with your project
Who maintains and contributes to the project

# Introduction

Any code used to deploy the client is PowerShell v5.1.  Since we are working with files in "c:\Program Files", PowerShell should be started with Admin privileges. 

![PowerShell Illustration ](images/PowerShell.png?raw=true)

User settings are stored in a *user's* profile and will not be destroyed by either uninstallation or installation. However, these files can be copied somewhere safe before installation and periodically. 

```
c:\users\<<SEID>>\AppData\*\SAS
```

# Use of this Document and Git Repo

The targeted response files is the only 

# Remove Old SAS Client Install

Because we are using automation to deploy the new entire SAS client (9.4M8), not upgrading all of the pieces, we need to delete any installed pieces from the client workstation.

Previously, installers with admin privileges could install a feature named SAS PC Files Server as a service.  This wasn't a part of the standard install and won't be part of the install in the future.  However, the service's presence will prevent a clean removal.

```
Stop-Service -Name 'SAS PC Files Server'  
```

Any future install will look to the *installer's* Windows profile for a record of the previous installation. The installation logs and records are stored in a folder named SASDeploymentWizard. Therefore, we will destroy any SASDeploymentWizard folders we can find.  During installation, monitor this directory.

```
Remove-Item -Recurse -Force -Path C:\Users\*\AppData\Local\SAS\SASDeploymentWizard

reg delete "HKLM\SOFTWARE\SAS Institute Inc." /f 

Remove-Item -Recurse -Force -Path 'C:\Program Files*\SASHome'
```
# Installation

Troubleshooting: the ResponseFile REQUIRES an entry with a full path to a license file.  The license files are stored at the root of \sas_software_depot\sid_files


![Example of a SAS Installation File](images/SASInstallationFile.png)

$ENV:OneDrive\Documents\sas_workstation_install_config\ResponseFiles\ResponseFile-Basic-EG64.txt

```
The responsefiles to be used for installation can be found in several features.

- ResponseFile-Basic-EG64.txt
- ResponseFile-Extended-EG64.txt

# $ResponseFile = ..\ResponseFiles\ResponseFile-Basic-EG64.txt

 $ResponseFile = ..\ResponseFiles\ResponseFile-Basic-EG64.txt

\ResponseFiles\ResponseFile-Basic-EG64.txt

'# $ResponseFile = C:\Users\Brett\Desktop\ResponseFile-Extended-EG32.txt
'# $ResponseFile = C:\Users\Brett\Desktop\ResponseFile-Extended-EG64.txt

C:\sas_software_depot\setup.exe -RESPONSEFILE $ResponseFile

Start-Process -filepath "c:\sas_software_depot\setup.exe" -ArgumentList '-RESPONSEFILE $ResponseFile'


Start-Process -filepath "C:\Users\swwcb\Desktop\sas_software_depot\setup.exe" -ArgumentList '-RESPONSEFILE C:\Users\BRETT\Desktop\ResponseFile-Extended-EG64.txt'

 msiexec.exe /i "F:\sas_software_depot\products\eguide__94200__wx6__en__sp0__1\eguide.msi" /qn /norestart DIR_APPFILES="C:\Program Files\SASHome\SASEnterpriseGuide\8" REG_FILETYPES="0" ARPSYSTEMCOMPONENT=1 REINSTALLMODE=amus /LV*X "F:\sas_software_depot\enterprise_guide_log.txt"
scmd

```
# Common Installation Issues

If any installation problems are encountered, then the entire C:\Users\<<SEIDad>>\AppData\Local\SAS\SASDeploymentWizard contents should be submitted to the CDWHelpDesk.

- Check for log entry c:\users<<siedad>>\AppData\Local\SAS\SASDeploymentWizard\SDW_YEAR_<datetime>.log reporting that the response file is invalid. MODIFY the ResponseFile to point the correct license file. 

- Windows 11

- 