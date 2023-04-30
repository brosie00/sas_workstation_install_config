
monitor usage
automate performance - up down

install git
backup settings files 

Robocopy.exe "\\WORK\users\Work\Desktop\sas_software_depot" C:\sas_software_depot  /E /mt:16

Stop-Service -Name 'SAS PC Files Server'  

Remove-Item -Recurse -Force -Path C:\Users\*\AppData\*\SAS\SASDeploymentWizard

reg delete "HKLM\SOFTWARE\SAS Institute Inc." /f 

Remove-Item -Recurse -Force -Path 'C:\Program Files*\SASHome'



-----------------------
INSTALLATION

-----------------------

Troubleshooting: the ResponseFile REQUIRES an entry with a full path to a license file.  If this 

```
# $ResponseFile = C:\Users\Brett\Desktop\ResponseFile-Basic-EG32.txt
 $ResponseFile = "C:\Users\Brett\Desktop\ResponseFile-Basic-EG64.txt" 


'# $ResponseFile = C:\Users\Brett\Desktop\ResponseFile-Extended-EG32.txt
'# $ResponseFile = C:\Users\Brett\Desktop\ResponseFile-Extended-EG64.txt

C:\sas_software_depot\setup.exe -RESPONSEFILE $ResponseFile

Start-Process -filepath "c:\sas_software_depot\setup.exe" -ArgumentList '-RESPONSEFILE $ResponseFile'


Start-Process -filepath "C:\Users\swwcb\Desktop\sas_software_depot\setup.exe" -ArgumentList '-RESPONSEFILE C:\Users\BRETT\Desktop\ResponseFile-Extended-EG64.txt'

 msiexec.exe /i "F:\sas_software_depot\products\eguide__94200__wx6__en__sp0__1\eguide.msi" /qn /norestart DIR_APPFILES="C:\Program Files\SASHome\SASEnterpriseGuide\8" REG_FILETYPES="0" ARPSYSTEMCOMPONENT=1 REINSTALLMODE=amus /LV*X "F:\sas_software_depot\enterprise_guide_log.txt"
scmd

```
SASHFADD Quick Start Guide for Windows
Complete these steps to use SASHFADD in Windows environments:
1. Download the SASHFADDwn.exe file. https://tshf.sas.com/techsup/download/hotfix/HF2/util01/SASHotFixDLM/tool/SASHFADDwn.exe
2. Launch the SASHFADDwn.exe installer, which installs SASHFADD in the C:\Program Files\SAS\SASHFADD directory.
3. Generate a DeploymentRegistry.txt, DeploymentRegistry.html  file for your SAS deployment as described in SAS Note 35968.  The default output will report only the current release of product components which are installed in the current SASHOME.
    * java -jar C:\Program Files\SASHome\deploymntreg\sas.tools.viewregistry.jar

4. Copy the generated DeploymentRegistry.txt to the same directory as the SASHFADD.exe file.
    copy-item "C:\Program Files\SASHome\deploymntreg\DeploymentRegistry.txt" "C:\Program Files\SAS\SASHFADD"

5. Double-click the SASHFADD.exe file, follow the on-screen instructions, and create three folders. One log directory, one location for downloaded hotfixes, one generated powershell .
                    PS C:\Program Files\SAS\SASHFADD> .\SASHFADD.exe

                    PS C:\Program Files\SAS\SASHFADD> .\SASHFADD.exe 
                    ** SAS Hot Fix Analysis, Download and Deployment Tool Ver. 2.2.4 **

                    Enter a descriptive name of the machine that contains the SAS deployment
                    or press "Enter" to accept a default name: 2023_May_Basic_EG64 

                    C:\Program Files\SAS\SASHFADD>powershell -Command "$ProgressPreference = 'SilentlyContinue';Invoke-WebRequest https://tshf.sas.com/techsup/download/hotfix/HF2/util01/SASHotFixDLM/data/SAS94_HFADD_data.xml -OutFile SAS94_HFADD_data.xml"

                    SASHFADD processing complete!

                    SASHFADD output written to directory:
                    -> 2023_May_Basic_EG64_2023_4_28_16.15.19


6. After SASHFADD finishes running, review the generated SAS_Hot_Fix_Analysis_Report_.
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

7. Double-click the powershell_script.bat file in the DOWNLOAD_ folder, which downloads all eligible hot fixes to the DEPLOY_ folder.
8. Launch the SAS® Deployment Manager, remembering any specific pre- or post-installation steps indicated by [D] in the SAS_Hot_Fix_Analysis_Report_ (step 6). 
    a. Click Apply Hot Fixes.
    b. When prompted, point the SAS® Deployment Manager to the DEPLOY_ folder containing the hot fixes that you downloaded in step 7.