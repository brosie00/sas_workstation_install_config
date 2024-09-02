
monitor usage
automate performance - up down

install git
backup settings files 

Robocopy.exe "\\WORK\users\Work\Desktop\sas_software_depot" C:\sas_software_depot  /E /mt:16




Viya 35
.\mirrormgr.exe mirror --deployment-data "C:\Users\Work\Desktop\SAS_Viya_deployment_data_2024_August.zip" --path "C:\Users\Work\Desktop\70255166-9CZVHF" --platform "x64-redhat-linux-6" --latest --log-file ".\logfile.txt"


-----------------------
INSTALLATION
-----------------------

Troubleshooting: the ResponseFile REQUIRES an entry with a full path to a license file.  If this 




# $ResponseFile = C:\Users\Brett\Desktop\ResponseFile-Basic-EG32.txt
 $ResponseFile = "C:\Users\Brett\Desktop\ResponseFile-Basic-EG64.txt"

# $ResponseFile = C:\Users\Brett\Desktop\ResponseFile-Extended-EG32.txt
# $ResponseFile = C:\Users\Brett\Desktop\ResponseFile-Extended-EG64.txt

C:\sas_software_depot\setup.exe -RESPONSEFILE $ResponseFile

Start-Process -filepath "c:\sas_software_depot\setup.exe" -ArgumentList '-RESPONSEFILE $ResponseFile'


Start-Process -filepath "C:\Users\swwcb\Desktop\sas_software_depot\setup.exe" -ArgumentList '-RESPONSEFILE C:\Users\BRETT\Desktop\ResponseFile-Extended-EG64.txt'

 msiexec.exe /i "F:\sas_software_depot\products\eguide__94200__wx6__en__sp0__1\eguide.msi" /qn /norestart DIR_APPFILES="C:\Program Files\SASHome\SASEnterpriseGuide\8" REG_FILETYPES="0" ARPSYSTEMCOMPONENT=1 REINSTALLMODE=amus /LV*X "F:\sas_software_depot\enterprise_guide_log.txt"
scmd

