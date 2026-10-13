# linux-commands-handbook

Navigation & Paths
pwd - Shows your current directory path so you don't get lost.
cd - Changes directories (e.g., cd /var/log or cd .. to go back).
ls - Lists files and folders. I usually run ls -la to see permissions and hidden files.
tree - Prints out directories in a tree diagram to visualize project structures.
which - Shows the exact binary path of a tool, like which git.
whereis - Locates the binary, source code, and man pages for a program.

File & Folder Operations

touch - Creates a new empty file quickly or updates timestamps.
mkdir - Makes a new folder. Use -p to make parent and child folders together.
cp - Copies files. Use cp -r to copy full directories.
mv - Renames files or moves them to another folder.
rm - Deletes files. 
rm -r deletes folders (be careful with -rf).
ln - Creates links between files (ln -s makes a soft/symbolic link).
find - Searches the filesystem for files matching names, types, or sizes.
locate - Quickly finds files using an indexed database.Reading & Working with Text
cat - Dumps the whole file content straight into the terminal.
tac - Prints a file in reverse, bottom line first.
less - Lets you scroll through big logs page by page without freezing memory.
more - A simple pager that scrolls forward through a file.
head - Shows the first 10 lines of a file by default.
tail - Shows the last lines of a file. 
tail -f streams live log updates.
grep - Searches for text patterns or words inside files.
wc - Word count. I mostly use wc -l to count total lines.
sort - Sorts lines of text alphabetically or numerically.
uniq - Removes duplicate lines from sorted input.
cut - Extracts specific columns or fields from CSV/delimited text.
awk - Useful for grabbing specific columns, like printing only column 1 and 3.
sed - Stream editor, mainly used for search-and-replace in files.
diff - Compares two files line by line and highlights differences.

echo - Prints text to the screen or appends it into files.

Permissions & Users

chmod - Changes read, write, and execute permissions on a file.
chown - Changes which user or group owns a file.
sudo - Runs a single command with root administrator privileges.
su - Switches to another user account in the terminal.
useradd - Adds a new user to the system.
usermod - Modifies user settings, like adding a user to the sudo group.
passwd - Sets or resets a user password.
whoami - Tells you which user you are currently logged in as.System, Disks & Processes
ps - Shows active processes. 
ps aux shows everything running on the system.
top - Interactive task manager showing live CPU and RAM usage.
kill - Stops a process using its Process ID (PID).
killall - Kills processes by name instead of looking up PIDs.
df - Disk filesystem space. 
df -h gives numbers in GB and MB.
du - Shows directory sizes on disk (du -sh gives a clean summary).
free - Shows free and used RAM memory (free -h).
uptime - Tells you how long the machine has been running without a reboot.
uname - Shows kernel and OS details (uname -a).

Networking

ping - Tests network connectivity and latency to another IP or domain.
curl - Fetches web pages or tests API endpoints from the terminal.
wget - Downloads files directly from the web via URL.
ssh - Securely connects into a remote server's terminal.
scp - Copies files securely between your computer and a remote server over SSH.
ss - Checks listening ports and network sockets (ss -tuln).

Archives & Manual

tar - Compresses or extracts .
tar.gz archive bundles.zip / unzip - Standard zip file compression and extraction.
gzip / gunzip - Compresses single files into .gz.
man - Opens the official manual page for any command so you can check flags.Weekend Homework 

TasksPart 1 — Linux Basics & File Management

Terminal Output$ 
whoami
khushi

$ hostname
devops-workstation

$ pwd
/home/khushi

$ date
Tue Oct 13 15:15:20 IST 2026

$ uname -a
Linux devops-workstation 6.8.0-45-generic #45-Ubuntu SMP PREEMPT_DYNAMIC x86_64 GNU/Linux

$ cat /etc/os-release
NAME="Ubuntu"
VERSION="24.04.1 LTS (Noble Numbat)"
ID=ubuntu

Purpose of each command:

whoami: Confirms my current user account.
hostname: Shows the server or machine name.
pwd: Prints the full directory path I am currently standing in.
date: Prints current system date and time.
uname -a: Prints OS kernel version, architecture, and machine info.
cat /etc/os-release: Shows the specific Linux distribution and version details.

Directory Setup$ 

mkdir -p linux-homework/{logs,scripts,reports}
$ cd linux-homework
$ touch logs/app.log
$ touch reports/summary.txt
$ ls -lR

.:
total 12
drwxr-xr-x 2 khushi khushi 4096 Oct 13 15:16 logs
drwxr-xr-x 2 khushi khushi 4096 Oct 13 15:16 reports
drwxr-xr-x 2 khushi khushi 4096 Oct 13 15:16 scripts

$ touch notes.txt
$ echo "My initial assignment notes" > notes.txt
$ cat notes.txt
My initial assignment notes

$ cp notes.txt reports/
$ mv reports/notes.txt reports/final_notes.txt
$ ls -l reports/
total 4
-rw-r--r-- 1 khushi khushi 28 Oct 13 15:17 final_notes.txt
-rw-r--r-- 1 khushi khushi  0 Oct 13 15:16 summary.txt
Conceptual Questions:What is Linux? It's an open-source operating system kernel created by Linus Torvalds that talks directly to computer hardware. Distributions combine the kernel with GNU system utilities to make a complete OS.OS vs. Terminal vs. Shell: The OS manages hardware and processes. The terminal is the window or app where you type. The shell (like bash) is the program inside that reads your commands and runs them.Absolute vs. Relative Path: An absolute path starts from the root / (e.g. /home/khushi/file.txt), so it works from anywhere. A relative path starts from where you are right now (e.g. reports/notes.txt).cp vs mv vs rm vs touch vs mkdir: cp copies a file, mv renames or moves it, rm deletes it, touch creates an empty file or refreshes timestamps, and mkdir creates folders.Part 2 — Users, Groups & PermissionsCommands & Outputs$ whoami
khushi

$ id
uid=1001(khushi) gid=1001(khushi) groups=1001(khushi),27(sudo)

$ touch linux-homework/scripts/test.sh
$ ls -l linux-homework/scripts/test.sh
-rw-r--r-- 1 khushi khushi 0 Oct 13 15:18 linux-homework/scripts/test.sh

$ chmod 644 linux-homework/scripts/test.sh
$ ls -l linux-homework/scripts/test.sh
-rw-r--r-- 1 khushi khushi 0 Oct 13 15:18 linux-homework/scripts/test.sh

$ chmod 755 linux-homework/scripts/test.sh
$ ls -l linux-homework/scripts/test.sh
-rwxr-xr-x 1 khushi khushi 0 Oct 13 15:18 linux-homework/scripts/test.sh
Answers:r is read (4), w is write (2), and x is execute (1).644 means the owner can read and write ($4+2=6$), while group and others can only read ($4$).755 means the owner can read, write, and execute ($4+2+1=7$), while group and others can read and execute ($4+1=5$).A script gets "Permission denied" if the execute bit (+x) is not set, or if the user doesn't have read access to the file or execute access on parent folders.sudo temporarily runs commands with root privileges. It should be used carefully because accidental typos or destructive commands run with root can break the entire operating system.No, chmod 777 makes it completely insecure. It gives everyone on the system full permission to edit, replace, or delete the file.Part 3 — Processes & ServicesCommands & Outputs$ ps aux | head -n 4
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1 169348 13120 ?        Ss   09:00   0:02 /sbin/init
root         2  0.0  0.0      0     0 ?        S    09:00   0:00 [kthreadd]

$ ps aux | grep ssh
root      1042  0.0  0.0  15828  7120 ?        Ss   09:00   0:00 sshd: /usr/sbin/sshd -D

$ systemctl status cron
● cron.service - Regular background program processing daemon
     Active: active (running) since Tue 2026-10-13 09:00:12 IST; 6h ago
   Main PID: 812 (cron)
Answers:A process is an active program running in memory.A PID is the unique Process ID number the kernel assigns to each running task.A process is any running program, while a service is a background daemon managed by the system (like systemd) that runs continuously without user intervention.systemctl start runs a service right now for this session only. systemctl enable configures it to start automatically whenever the server boots up.If a service is inactive, I would check its status with systemctl status <service>, inspect recent error logs using journalctl -u <service>, check if its port is blocked, and test config file syntax.
