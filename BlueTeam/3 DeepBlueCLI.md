# DeepBlueCLI 
https://github.com/sans-blue-team/DeepBlueCLI


## Tool that shows malicious and suspicious logs, also works well on a domain controller
### Keep in mind, logs might not exist if the actor purged the event log
#### They do this by running "wevtutil cl <logname>" or "Remove-EventLog -LogName <logname>"
##### This does leave an Event 104 "The <logname> log file was cleared" event in System log


1) Copy DeepBlueCLI-master directory to suspect machine
2) open powershell and cd to location of DeepBlue.ps1
3) run `Set-ExecutionPolicy unrestricted`

`.\DeepBlue.ps1 -log security | Out-GridView`

`.\DeepBlue.ps1 -log system | Out-GridView`

`.\DeepBlue.ps1 -log application | Out-GridView`

`.\DeepBlue.ps1 -log powershell | Out-GridView`
