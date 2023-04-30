# Overview
- Inventory of installed SAS elements
- Export the inventory to a non-IRS workstation with direct Internet access
- Use a sas tool to process the inventory and automate the list of needed hotfixes
- 
# SASHFADD Quick Start Guide for Windows
Complete these steps to use SASHFADD in Windows environments:

# IRS Machine

1. From an IRS windows machine,  Generate a DeploymentRegistry.txt, DeploymentRegistry.html  file for your SAS deployment as described in SAS Note 35968.  The default output will report only the current release of product components which are installed in the IRS windows machine's current SASHOME.
```
    java -jar java -jar "C:\Program Files\SASHome\deploymntreg\sas.tools. viewregistry.jar"
```
# Non-IRS Machine 

1. Download the SASHFADDwn.exe from the SAS Website file to a machine with Internet Access. https://tshf.sas.com/techsup/download/hotfix/HF2/util01/SASHotFixDLM/tool/SASHFADDwn.exe
2. Launch the SASHFADDwn.exe installer and install SASHFADD in the C:\Program Files\SAS\SASHFADD directory. This file is the default and is different than C:\Program Files\SASHome. 

4. Copy the generated DeploymentRegistry.txt to the same directory as the SASHFADD.exe file.
    copy-item "C:\Program Files\SASHome\deploymntreg\DeploymentRegistry.txt" "C:\Program Files\SAS\SASHFADD"

5. Either, Double-click the SASHFADD.exe file, follow the on-screen instructions, and create three folders. One log directory, one location for downloaded hotfixes, one generated powershell .  

SASHFADD can also be launched via a powershell command line.

        PS C:\Program Files\SAS\SASHFADD> .\SASHFADD.exe
```
        PS C:\Program Files\SAS\SASHFADD> .\SASHFADD.exe 
        ** SAS Hot Fix Analysis, Download and Deployment Tool Ver. 2.2.4 **

        Enter a descriptive name of the machine that contains the SAS deployment
        or press "Enter" to accept a default name: 2023_May_Basic_EG64 

        C:\Program Files\SAS\SASHFADD>powershell -Command "$ProgressPreference = 'SilentlyContinue';Invoke-WebRequest https://tshf.sas.com/techsup/download/hotfix/HF2/util01/SASHotFixDLM/data/SAS94_HFADD_data.xml -OutFile SAS94_HFADD_data.xml"

        SASHFADD processing complete!

        SASHFADD output written to directory:
            -> 2023_May_Basic_EG64_2023_4_28_16.15.19
```

1. After SASHFADD finishes running, review the generated SAS_Hot_Fix_Analysis_Report_.
• Take note of any hot fixes in the SAS_Hot_Fix_Analysis_Report_ indicated by [D] because these fixes require additional pre- or post-installation steps that must be completed during step 8.

    PS C:\Program Files\SAS\SASHFADD\SASHFADD_2023_4_28_16.04.40> tree
Folder PATH listing for volume Local Disk
Volume serial number is EE93-C8BA
|       MD5_checksums.txt
|       MD5_checksums_ALERT_ONLY.txt
|       powershell_script.bat
|       powershell_script_ALERT_ONLY.bat
|
\---LOG_SASHFADD_2023_4_28_16.04.40
        Installed_Hot_Fixes_SASHFADD_2023_4_28_16.04.40.html
        Installed_Hot_Fixes_SASHFADD_2023_4_28_16.04.40.xml
        SASHFADD_LOG_2023_4_28_16.04.40.txt

1. Double-click the powershell_script.bat file in the DOWNLOAD_ folder, which downloads all eligible hot fixes to the DEPLOY_ folder.
2. Launch the SAS® Deployment Manager, remembering any specific pre- or post-installation steps indicated by [D] in the SAS_Hot_Fix_Analysis_Report_ (step 6). 
    a. Click Apply Hot Fixes.
    b. When prompted, point the SAS® Deployment Manager to the DEPLOY_ folder containing the hot fixes that you downloaded in step 7.


