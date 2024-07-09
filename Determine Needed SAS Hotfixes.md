# Introduction  
SAS releases hotfixes to address security needs.  Unlike Windows or Microsoft Office, there is no monolithic installer or updater. Since each install might be completely different, SAS requires an inventory of the existing installation and then compares that inventory to a list of available hotfixes.

# Overview 
- Inventory the SAS Installation
- Export the inventory to a non-IRS workstation with direct Internet access
- Use a sas tool to process the inventory and automate the list of needed hotfixes
- Use a script to download the hotfixes
- Move the hotfixes to an IRS workstation
- Install hotfixes
- 
# SASHFADD Quick Start Guide for Windows
Complete these steps to use SASHFADD in Windows environments:

# IRS Machine

1. As and ADMINISTRATOR and from an IRS windows machine with an existing SAS installation, generate a DeploymentRegistry.txt and a DeploymentRegistry.html file using tools already present in the install. The full method is described in [SAS Note 35968.](https://support.sas.com/kb/35/968.html). The default output will report only the current release of product components which are installed in the IRS windows machine's current SASHOME.

From a cmd prompt ( !NOT PowerShell, due to parsing issues) and as administrator,
```
    cd "C:\Program Files\SASHome\deploymntreg"
    "C:\Program Files\SASHome\SASPrivateJavaRuntimeEnvironment\9.4\jre\bin\java.exe" -jar "C:\Program Files\SASHome\deploymntreg\sas.tools.viewregistry.jar"
```
Which will create 2 DeploymentRegistry* files.

```
    Directory: C:\Program Files\SASHome\deploymntreg

    Mode                 LastWriteTime         Length Name
    ----                 -------------         ------ ----
    -a---           4/30/2023  3:19 PM          66585 DeploymentRegistry.html
**  -a---           4/30/2023  3:19 PM          34493 DeploymentRegistry.txt**
    -a---           4/29/2023  4:25 PM         347111 registry.jnl
    -a---           4/29/2023  4:14 PM              0 registry.lck
    -a---           4/29/2023  4:14 PM             49 registry.properties
    -a---           4/29/2023  4:25 PM         252578 registry.xml
    -a---           1/19/2023  3:54 AM          27033 sas.tools.deploymntreg.jar
    -a---           1/19/2023  3:54 AM           9214 sas.tools.viewregistry.jar

```
# Non-IRS Machine 

1. Download the current version of the SASHFADDwn.exe from the SAS Website file to a machine with Internet Access. https://tshf.sas.com/techsup/download/hotfix/HF2/util01/SASHotFixDLM/tool/SASHFADDwn.exe

2. As an Administrator, launch the SASHFADDwn.exe installer and install SASHFADD in the "C:\Program Files\SAS\SASHFADD" directory. This file is the default and **is different than C:\Program Files\SASHome. **

3. As an Administrator, Copy the generated DeploymentRegistry.txt to "C:\Program Files\SAS\SASHFADD"
   ```
   Copy-Item "C:\Program Files\SASHome\deploymntreg\DeploymentRegistry.txt" "C:\Program Files\SAS\SASHFADD"
   ```

4. As an Administrator, Either, Double-click the SASHFADD.exe file, follow the on-screen instructions, and create three folders. One log directory, one location for downloaded hotfixes, one generated powershell .  

SASHFADD can also be launched via a powershell command line.  Choose a  descriptive name of the machine that contains the SAS deployment ( 2023_May_Basic_EG64 ) or press "Enter" to accept a default name:

```
& 'C:\Program Files\SAS\SASHFADD\SASHFADD.exe'

** SAS Hot Fix Analysis, Download and Deployment Tool Ver. 2.2.4 **

Enter a descriptive name of the machine that contains the SAS deployment
or press "Enter" to accept a default name: 2023_May_Basic_EG64

C:\Program Files\sas\SASHFADD>powershell -Command "$ProgressPreference = 'SilentlyContinue';Invoke-WebRequest https://tshf.sas.com/techsup/download/hotfix/HF2/util01/SASHotFixDLM/data/SAS94_HFADD_data.xml -OutFile SAS94_HFADD_data.xml"

SASHFADD processing complete!

SASHFADD output written to directory:
 -> 2023_May_Basic_EG64_2023_4_30_17.16.31

```
5. After SASHFADD finishes running, review the generated SAS_Hot_Fix_Analysis_Report_* cretead in the new directory.
• Take note of any hot fixes in the SAS_Hot_Fix_Analysis_Report_ indicated by [D] because these fixes require additional pre- or post-installation steps that must be completed during step 8.
```
PS C:\Program Files\sas\SASHFADD> tree /f                                                                                                                                                     Folder PATH listing for volume BOOTCAMP
Volume serial number is 8CB2-AE79
C:.
│   DeploymentRegistry.html
│   DeploymentRegistry.txt
│   SAS94_HFADD_data.xml
│   SAS94_HFADD_data_powershell_download.bat
│   SASHFADD.cfg
│   SASHFADD.exe
│
└───2023_May_Basic_EG64_2023_4_30_17.16.31
    │   SAS_Hot_Fix_Analysis_Report_2023_4_30_17.16.31.html
    │
    ├───DEPLOY_2023_May_Basic_EG64_2023_4_30_17.16.31
    │       INSTALL_README.txt
    │
    ├───DOWNLOAD_2023_May_Basic_EG64_2023_4_30_17.16.31
    │       ALERT_README.txt
    │       MD5_checksums.txt
    │       MD5_checksums_ALERT_ONLY.txt
    │       powershell_script.bat
    │       powershell_script_ALERT_ONLY.bat
    │
    └───LOG_2023_May_Basic_EG64_2023_4_30_17.16.31
            Installed_Hot_Fixes_2023_May_Basic_EG64_2023_4_30_17.16.31.html
            Installed_Hot_Fixes_2023_May_Basic_EG64_2023_4_30_17.16.31.xml
            SASHFADD_LOG_2023_4_30_17.16.31.txt


```

6. Double-click the powershell_script_ALERT_ONLY.bat file in the DOWNLOAD_* folder, which downloads all eligible hot fixes to the DEPLOY_ folder.  SAS overthrought the steps of downloading the hotfixes.  It is just easier to look for the urls and open them up in seperate MS Edge windows. 

7. Launch the SAS® Deployment Manager, remembering any specific pre- or post-installation steps indicated by [D] in the SAS_Hot_Fix_Analysis_Report_ (step 6). 
    a. Click Apply Hot Fixes.
    b. When prompted, point the SAS® Deployment Manager to the DEPLOY_ folder containing the hot fixes that you downloaded in step 7.


