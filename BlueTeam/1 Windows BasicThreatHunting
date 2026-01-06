#####Windows Basic Command Line Threat Hunting#####
#Start with network connections and go from there

netstat -anob
#List connections and process ID/executable. Look for ESTABLISHED

netstat -f
#Show resolved domains in connections

tasklist /svc
#All executables and services associated - find what that svchost.exe actually is

tasklist /m
#All executables and the .dll files associated

tasklist /m <name>.dll 
#list all executables that are running a specific .dll files

tasklist /m /fi "pid eq <PID>"
#List all .dll files for a specific executable

wmic process where processid=<PID> get commandline
#Get command line that launched the process

wmic process get name,parentprocessid,processid | find "<PID>"
#See what spawned the process

#####Persistence and Auto-Start Extensibility Points (ASEPs)#####
#Run Keys
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce

#Shell Keys
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders

#Services Keys
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunServices

#Policy Keys
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run

#Logged in user Keys
HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows

#Boot Key
By default, the multistring BootExecute value of the registry key HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Session Manager is set to autocheck autochk *. 
This value causes Windows, at startup, to check the file-system integrity of the hard disks if the system has been shut down abnormally. 
Adversaries can add other programs or processes to this registry value which will automatically launch at boot.

#Startup Folders
C:\Users\[Username]\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp

#Drivers
Windows Event Logs:
Event ID 3000-3006: Logs metadata about driver signature validation.
Event ID 2000-2011 (Windows Defender Application Control): Tracks driver integrity and policy enforcement.
PowerShell: Use commands to retrieve metadata about installed drivers: Get-WindowsDriver -Online | Select-Object Driver, ProviderName, Version

#Services

#Scheduled Tasks

#####EVENT IDs#####
4688 Security - CMD line in process creation events (logging needs to be enabled for this one)
4624 Security - Successful Logon
4625 Security - Failed Login
4720 Security - A user account was created
4728 Security - A member was added to a security-enabled global group
4732 Security - A member was added to a security-enabled local group
4756 Security - A user added to security enabled universal group
4776 Security - Successful /Failed Account Authentication
4778 Security - RDP reconnected
4779 Security - RDP disconnected
7030 System - Service Creation Errors
7045 System - Service Creation
4722 Security - A user account was enabled
4724 Security - An attempt was made to reset an account's password
4738 Security - A user account was changed
4735 Security - A Security-enabled local group was changed
4755 Security - A Security-enabled universal group was changed
4697 Security - A service was installed
