# Linux hunting
## Start with network connections and go from there

#### List open files:
`lsof -i -P`

#### find network connections
`lsof -p <processID>`

#### List processes WITH the command line that launched them
`ps aux`

#### If you find a suspicious process, you can cd to that pid and then use strings to examine the files
`cd /proc/[pid]`
`ls`
`strings ./<file> | less`

#### Find all files associated with listener
`cd /proc/<processID>`
`strings ./<file>`

#### If lots of noise, choose a minimum length of maybe 6? Warning: might not see important other short strings.
`strings -n 6 malware.exe > output.txt`
Google errors that you find

#### List open file, show files unlinked/deleted, you can still see it in /proc/<processID>
`lsof +L1`

#### records the source IP, destination IP, and other information of a TCP connection in the ESTABLISHED state
`/proc/net/nf_conntrack | less`


## OTHER USEFUL LINUX COMMANDS
`top` → Display current running processes
`pstree` → Display a tree of processes
`find` → Find files and directories
##### Example of find command. Find all .txt files in entire system and hide permission denied errors:
`find / -name "*.txt" 2>/dev/null`

`dnf list installed` → Display installed packages
`yum list installed` → Display installed packages
`dpkg -l` → Display installed packages

`ext4magic` → List/recover deleted files

`.bash_history` → Get the command history for the Bash shell
`.mysql_history` → Get the query history for the MySQL/MariaDB sessions
`.ftp_history` → Get the command history for the FTP (File Transfer Protocol) client
`.git/logs` → Get log files that track changes to the repository’s references and branches
`/etc/passwd` → Get essential information about user accounts
`/etc/group` → Get essential information about user groups

`/etc/cron*` `/var/cron*` `/etc/at*` → Linux scheduler

## LINUX LOGS
`/var/log/messages` → Contains global system messages, including the messages that are logged during system startup

`/var/log/auth.log` → Authentication logs

`/var/log/kern.log` → Kernel information and events

`/var/log/secure` → Authentication logs

`/var/log/syslog` → Contains messages that are recorded by the host about the system activity

`/var/log/httpd/` → Apache logs

`/var/log/daemon.log` → Contains information about running system and application daemons

`/var/log/cron` → Cron logs

`/var/log/auditd/audit.log | grep denied` → Get SELinux alerts

`/var/log/journal` → journald systemd's logs

`journalctl --file X.journal -o verbose > journal.txt` → Dump journald logs with verbose output
