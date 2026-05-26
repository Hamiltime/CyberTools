# Power Decode
https://github.com/Malandrone/PowerDecode
#### Tip: BurpSuite has a decoder/encoder that works as good as, if not better, than CyberChef.

## SETUP
PowerDecode takes a .ps1 or powershell within a .txt file and de-ofuscates it

1) Enable scripts execution: launch PowerShell as Administrator and run the command:

`Set-ExecutionPolicy bypass`

2) If it doesn't work, open Registry Editor as Administrator and go to:

`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\PowerShell`

Set the parameter "ExecutionPolicy" on value "Bypass"

3) Disable any antivirus software in order to allow the tool to analyze malware without interruption.

4) Click on PowerDecode.bat to start the GUI

## DECODE

#### After opening the GUI
1) Choose option number 1 "Automatic decode mode"
2) Choose option number 1 "Decode a script from a single file"
3) Choose the .ps1 or .txt with the obfuscated powershell text
4) Choose an output folder for the results
5) Open the results in Notepad++ or similar to easily read the code
