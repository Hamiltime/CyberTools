# REMnux EXE Analysis

File analysis is about finding clues and making assumptions, it is difficult to know exactly what the file is executing and many of these commands may not return useful information. 
Keep trying and use each tool to find clues about the EXE behavior. 

#### Search through document
`strings <FileName> | grep -i <SearchTerm>`

#### Basic Identificaiton
`File <FileName>`

More Identification
`exiftool -a -u -g1 <FileName>`

#### Search through Document or EXE and filter out meaningless small strings and noise
`strings -n 8 <FileName>`

#### One of the more useful tools, the peframe tool is used to perform static analysis on “Windows PE (Portable Executable)” files to gather information about its characteristics, potential indicators of compromise, and other details that can aid in understanding its behavior.
`peframe <FileName>`

#### We can collect similar evidence using the pecheck tool.
`pecheck <FileName>`

#### We can collect strings as well from the exe
`pestr <FileName>`

#### TrID is a tool for identifying file types based on their binary signatures.
`trid <FileName> -v`

#### Running yara-rules against a sample can help identify known malware families or characteristics based on predefined rules.
`yara-rules <FileName>`

`Yara Rules Reference:

network_http: Indicates the presence of HTTP-related network functionality. The executable likely performs HTTP requests.

win_registry: Suggests interactions with the Windows Registry, possibly for configuration or persistence.

win_token: Indicates the use of Windows security tokens, potentially for privilege escalation or impersonation.

win_files_operation: The executable performs file operations, such as reading, writing, or modifying files.

Str_Win32_Wininet_Library: Indicates the use of the Wininet library, which provides functions for Internet client applications.

Str_Win32_Internet_API: Confirms the use of Internet APIs, which supports network communications.

Str_Win32_Http_API: Further confirms the use of HTTP APIs for network communications.

ScanBox_Malware_Generic: Generic detection for ScanBox malware, indicating potential data exfiltration or reconnaissance activities.

suspicious_packer_section: The executable contains sections typical of packed files, which can be used to obfuscate the payload.

IsPE32: Confirms the file is a PE32 executable.

IsWindowsGUI: Confirms the executable is a Windows GUI application.

HasOverlay: The file contains overlay data, which may include appended data that is not part of the original program.

HasDigitalSignature: The executable has a digital signature, which could be legitimate or maliciously altered.

HasModified_DOS_Message: The DOS stub message has been modified, which can be a sign of tampering or an attempt to avoid detection.

IsGoLink: Indicates the use of the GoLink linker, which is less common and might suggest custom compilation.`

#### Attempt to unpack the exe to see if we can see whats inside
`upx -d <FileName>`

#### Scanning the file with clamscan can return additional information about the malware
(If you get cli_loaddbdir() error, this means clamscan needs to be updated. Run this command first: `freshclam`)
`clamscan <FileName> --allmatch=no -v`

#Use signsrch to see if there is an RSA key, which means the file is encrypted. This just verifies encryption is used
signsrch <FileName>

#We may be able to extract strings that are encoded with little endian
strings --encoding=l <FileName>

#To extract the overlay of a PE file into a separate file using pecheck, you can run the command
pecheck -g o -D <FileName> > sample.exe.test.overlay
strings <FileName>.test.overlay | less
strings --encoding=l <FileName>
hexdump -C <FileName>.test.overlay | less
#Note: “Overlay Extraction” refers to the process of isolating and extracting the overlay portion of a Portable Executable (PE) file. 
#An overlay is any data appended to the end of a PE file after the actual executable content. 
#This data is not part of the main executable sections and can contain various types of information, such as additional code, configuration data, or even malicious payloads.

#We can use the xorsearch tool for searching for any web traffic
xorsearch <FileName> http

#The brxor.py script can be used to search for and decode XOR-encoded strings within a binary.
brxor.py <FileName>

#The bbcrack tool extracts obfuscated data and attempts to crack it
bbcrack <FileName>

#The floss tool is similar and designed to extract and decode obfuscated strings from malware binaries. Look for User-Agents, Registry items and HTTP protocols.
floss --no=static <FileName>

#The capa tool provides a detailed analysis of the file based on its capabilities and behavior.
capa <FileName> -vv






