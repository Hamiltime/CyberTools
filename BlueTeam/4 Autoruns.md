# Autoruns
Download:
https://learn.microsoft.com/en-us/sysinternals/downloads/sysinternals-suite?source=recommendations

## When Autoruns opens, press Esc to cancel the current scan.
1) When looking for malware, it helps to be signed in as the user that got infected. If an admin account is signed in instead of the user, select User in the top menu, and select the correct user account.
2) Select Options and tick Hide Microsoft Entries.
# WARNING: DO NOT USE VIRUSTOTAL IF YOU ARE PARTICIPATING IN TRAINING EXERCISES SUCH AS TATANKA
4) Select Options > Scan Options, then tick Verify code signatures, Check VirusTotal.com and Submit Unknown Images.
5) Press F5 to start a new scan.

## If you wish to save the logs and view them on another system, you can perform the following:
When the scan is completed, click File > Save and save the log file as a .arn file.

## As far as identifying new malware, the things to look out for are:
-No description

-No publisher

-Normally an executable file (.exe)

-File name made up of random letters and numbers

-A google of the file name returns no results

-Multiple load points

-Encoded commands


## You can use the command line version: `autorunsc`
Usage: `autorunsc [-a *] [-c|-ct] [-h] [-m] [-s] [-u] [-vt] [[-z ] | [user]]]`

-c	Print output as CSV.
-ct	Print output as tab-delimited values.
-h	Show file hashes.
-m	Hide Microsoft entries (signed entries if used with -v).
-s	Verify digital signatures.
-t	Show timestamps in normalized UTC (YYYYMMDD-hhmmss).
-u	If VirusTotal check is enabled, show files that are unknown by VirusTotal or have non-zero detection, otherwise show only unsigned files.
-x	Print output as XML.
-v[rs]	Query VirusTotal for malware based on file hash. Add ‘r’ to open reports for files with non-zero detection. Files reported as not previously scanned will be uploaded to VirusTotal if the ‘s’ option is specified. Note scan results may not be available for five or more minutes.
-vt	Before using VirusTotal features, you must accept the VirusTotal terms of service. If you haven’t accepted the terms and you omit this option, you will be interactively prompted.
-z	Specifies the offline Windows system to scan.
user	Specifies the name of the user account for which autorun items will be shown. Specify ‘*’ to scan all user profiles.

EXAMPLE: autorunsc.exe -a * -s -c -h > autoruns_malware_report.csv



