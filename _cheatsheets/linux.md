---
layout: cheatsheet
title: "Linux Commands"
---

## Basic Commands

| Command                    | Description                                           |
|----------------------------|-------------------------------------------------------|
| `ls -l`                    | List directory contents in long format                |
| `ls -a`                    | Show all files, including hidden                      |
| `ls -h`                    | Show file sizes in human-readable format              |
| `ls -R`                    | Recursively list subdirectories                       |
| `dir`                      | Display files in directory                            |
| `uname -a`                 | Show system info                                      |
| `dmidecode`                | Decode hardware info                                  |
| `hostname `                | Show the hostname                                     |
| `uptime   `                | Show system uptime                                    |
| `whoami`                   | Show current user                                     |
| `who`                      | Show logged-in user                                   |
| `id`                       | Show UID, GID, and groups                             |
| `history`                  | Show command history                                  |
| `stat file`                | Detailed info about a file                            |
| `file name`                | Identify file type                                    |
| `basename path`            | Extract filename from path                            |
| `dirname path`             | Extract directory from path                           |
| `echo $?`                  | Show last command's exit status (0 = OK)              |
| `alias ll='ls -la'`        | Create command shortcut                               |
| `cd /path`                 | Change directory                                      |
| `cd` or `cd ~`             | Go to home directory                                  |
| `cd `                      | Go one level up                                       |
| `cd /`                     | Go to root                                            |
| `more filename`            | View file (forward only)                              |
| `less filename`            | View file with scroll                                 |
| `head -1 filename`         | View first line of file                               |
| `tail -1 filename`         | View last line of file                                |
| `cat > filename`           | Create new file                                       |
| `cat filename`             | Show file content                                     |
| `cat file1 file2 > file3`  | Merge files                                           |
| `mv file path/`            | Move file                                             |
| `mv old new`               | Rename file                                           |
| `mkdir name`               | Create directory                                      |
| `rm file`                  | Delete file                                           |
| `rmdir name`               | Delete empty directory                                |
| `rm -d`                    | Remove non-empty directory                            |
| `rm -rf`                   | Force delete directory and contents                   |
| `pr -x`                    | Format file into x columns                            |
| `pr -h`                    | Add header                                            |
| `pr -n`                    | Add line numbers                                      |
| `clear`                    | Clear the terminal                                    |

## File Permission Commands

| Command                   | Description                                                     |
|---------------------------|-----------------------------------------------------------------|
| `r`, `w`, `x`             | Read, Write, Execute permission                                 |
| `chmod 755 file`          | Set permissions to rwxr-xr-x                                    |
| `chmod +x scriptsh`      | Make script executable                                           |
| `-`                       | No permission                                                   |
| `chroot`                  | chroot swaps your view of / to somewhere else (like /media/sda1)|
| `chown user file`         | Change file owner                                               |
| `chown user:group file`   | Change owner and group                                          |
| `chmod u+x file`          | Give execute permission to owner                                |
| `chmod go-w file`         | Remove write permission from group/others                       |
| `chmod 664 file`          | rw-rw-r-- permission                                            |
| `find  -type f -perm 777` | Find all world-writable files                                   |
| `chgrp group file`        | Change group ownership                                          |
| `umask`                   | Show default permission mask                                    |

## Environment Variables

| Command                  | Description                                   |
|--------------------------|-----------------------------------------------|
| `echo $VAR`              | Display variable value                        |
| `env`                    | Show all environment variables                |
| `VAR=value`              | Set variable                                  |
| `unset VAR`              | Delete variable                               |
| `export VAR=value`       | Create/Set variable                           |
| `printenv VAR`           | Show specific environment variable            |
| `set`                    | Show all shell variables                      |
| `PATH=$PATH:/new/path`   | Add directory to PATH                         |
| `env | grep VAR`         | Search for a specific environment variable    |
| `declare -x VAR=value`   | Declare and export a variable (Bash)          |
| `printenv`               | Same as `env` but more script-friendly        |


## User Management

| Command                             | Description                                  |
|-------------------------------------|----------------------------------------------|
| `sudo adduser user`                 | Add a new user                               |
| `sudo passwd user`                  | Change user password                         |
| `sudo passwd -l 'user'`             | Lock user password                           |
| `passwd -d 'user'`                  | Delete user password                         |
| `passwd -e 'user'`                  | Force user to change password at next login  |
| `sudo userdel -r 'user'`            | Remove user                                  |
| `sudo usermod -aG GROUP USER`       | Add user to group                            |
| `sudo deluser USER GROUP`           | Remove user from group                       |
| `groups`                            | Show groups for current user                 |
| `id user`                           | Show UID, GID, and group info                |
| `id user`                           | Show UID, GID, and group info                |
| `last`                              | Show last login sessions                     |
| `who -u`                            | List active user sessions with idle times    |
| `w`                                 | Show who's logged in and what they’re doing  |
| `su - username`                     | Switch user and load their environment       |
| `getent passwd user`                | Get user info from `/etc/passwd`             |
| `finger`                            | Show logged-in users                         |
| `finger user`                       | Show user info                               |

## Disk and Filesystem Management

| Command                | Description                                       |
|------------------------|---------------------------------------------------|
| `mount /dev/sda1 /mnt` | Mount a filesystem manually to a directory        |
| `umount /mnt`          | Unmount a mounted filesystem                      |
| `fsck /dev/sda1`       | Check and repair filesystem errors on a partition |
| `df -h`                | Show disk space usage in human-readable form      |
| `du -sh /path`         | Show total size of a directory                    |
| `lsblk`                | Show block devices (disks, partitions)            |
| `blkid`                | Show UUID and filesystem type of block devices    |

## Forensics and File Recovery

| Command                              | Description                                                                               |
|--------------------------------------|-------------------------------------------------------------------------------------------|
| `find / -name filename`              | Find a file anywhere on the system                                                        |
| `find / -mtime -1`                   | Find files modified in the last 1 day                                                     |
| `grep -r 'keyword' /path`            | Search recursively for keywords inside files (eg, malware indicators, hidden configs)     |
| `strings file`                       | Extract readable ASCII strings from a binary file (good for malware and hidden messages)  |
| `file filename`                      | Determine the type of a file (text, executable, image, etc)                               |
| `lsattr file`                        | Show file attributes (like immutable, append-only)                                        |
| `chattr +i file`                     | Make a file immutable (even root can't delete it easily)                                  |
| `stat file`                          | Show detailed metadata (timestamps, ownership, permissions) for a file                    |
| `md5sum file`                        | Generate MD5 hash of a file (for integrity checks or digital evidence)                    |
| `sha256sum file`                     | Generate SHA-256 hash of a file (stronger integrity check)                                |
| `lsof`                               | List open files and what process is using them (good for live forensics)                  |
| `lsof -i`                            | Show network connections and related files/processes                                      |
| `cat /proc/mounts`                   | View all mounted filesystems (can help find rogue mounts or hidden partitions)            |
| `foremost -i imagedd -o output_dir`  | Carve files from a disk image (useful for recovering deleted files)                       |
| `photorec`                           | Recover deleted files from disks (powerful recovery tool, comes with `testdisk`)          |




## Networking

| Command                          | Description                                  |
|----------------------------------|----------------------------------------------|
| `ip a`                           | Show IP addresses                            |
| `ifconfig`                       | Show network interfaces                      |
| `ping 8888`                      | Send ICMP ping                               |
| `hostname -I`                    | Get local IP address                         |
| `ip route`                       | Show routing table                           |
| `arp -a`                         | Show ARP table                               |
| `nc -zv host port`               | Check if port is open                        |
| `telnet host port`               | Test socket connectivity (old school)        |
| `ss -s`                          | Summary of socket statistics                 |
| `nslookup http://pwnhublol`      | DNS lookup                                   |
| `dig http://pwnhublol`           | DNS query                                    |
| `traceroute http://pwnhublol`    | Show route path to host                      |
| `netstat -tuln`                  | Show open ports and services                 |
| `ss -tuln`                       | Like netstat but faster                      |
| `curl http://pwnhublol`          | Fetch URL content                            |
| `wget http://pwnhublol`          | Download file from URL                       |
| `scp file user@host:/path`       | Secure copy to remote host                   |
| `ftp`, `sftp`                    | File transfer protocols                      |
| `nmap target_ip`                 | Network scan                                 |
| `ssh user@host`                  | Connect via SSH                              |
| `ping host`                      | Ping test                                    |
| `put file`                       | Upload file (FTP/SCP)                        |
| `get file`                       | Download file                                |
| `quit`                           | Exit session                                 |


## Process Management

| Command              | Description                                       |
|----------------------|---------------------------------------------------|
| `bg`                 | Send process to background                        |
| `fg`                 | Bring process to foreground                       |
| `top`                | Real-time process viewer                          |
| `htop`               | Enhanced process viewer (if installed)            |
| `ps`                 | Show process list                                 |
| `ps aux`             | All running processes                             |
| `ps PID`             | Show info on specific process                     |
| `pidof name`         | Get PID of a process                              |
| `kill PID`           | Terminate process                                 |
| `killall name`       | Kill all processes by name                        |
| `nice`               | Start process with priority                       |
| `nice -n 10 command` | Run with low priority                             |
| `renice`             | Change priority of running process                |
| `renice -n 5 -p PID` | Change running process priority                   |
| `jobs`               | Show backgrounded jobs                            |
| `fg`, `bg`           | Move jobs foreground/background                   |
| `watch -n 1 command` | Repeat command every second                       |
| `df`                 | Show disk usage                                   |
| `free`               | Show memory usage                                 |
| `pgrep name`         | Get PID by process name                           |
| `pkill name`         | Kill all processes by name                        |
| `xargs kill`         | Mass-kill from list                               |
| `strace -p PID`      | Trace system calls from process                   |
| `lsof -p PID`        | List open files by process                        |
| `time command`       | Measure command execution time                    |

## Text Processing / Filters

| Command                     | Description                                |
|-----------------------------|--------------------------------------------|
| `cut -c1-2 file`            | Extract specific character columns         |
| `awk '{print $1}'`          | Print first column                         |
| `grep pattern file`         | Search for pattern                         |
| `sort options file`         | Sort file                                  |
| `sort file`                 | Sort lines alphabetically                  |
| `uniq file`                 | Remove duplicate lines                     |
| `uniq`                      | Remove duplicate lines (use after sort)    |
| `wc options file`           | Count lines, words, and bytes              |
| `wc -l file`                | Count lines                                |
| `paste file1 file2`         | Merge lines of files side by side          |
| `diff file1 file2`          | Show differences between two files         |
| `comm file1 file2`          | Compare sorted files line-by-line          |
| `xargs`                     | Build and execute command lines from input |
| `tee file`                  | Output to terminal and write to file       |
| `yes | command`             | Auto-confirm prompts                       |
| `cat file`                  | Show entire file content                   |
| `tac file`                  | Reverse cat                                |
| `head -n 10 file`           | First 10 lines                             |
| `tail -n 10 file`           | Last 10 lines                              |
| `cut -d':' -f1 /etc/passwd` | Cut field by delimiter                     |
| `nl file`                   | Number each line                           |
| `tr 'a-z' 'A-Z' < file`     | Translate lowercase to uppercase           |
| `sed 's/foo/bar/g' file`    | Replace text with sed                      |
