
### CheatSheet: Linux Commands for DevOps | by Vinodha Kumara | Medium

> ## Excerpt
> Absolutely! As a DevOps professional, it’s vital to be proficient in the Linux command line for effective server management, automation, and troubleshooting. In this comprehensive guide, we’ll cover…


1.  `**id**` - This is used to find out user and group names and numeric ID’s (UID or group ID) of the current user or any other user in the server.  Example: `id -u root`

2\. `**cd**` - Change Directory: Navigate to a different directory.  
Example:`cd /home/user/documents`

3\. `**pwd**` - Print Working Directory: Display the current directory's full path. Example: `pwd`

4\. `**mkdir**` - Make Directory: Create a new directory.  
Example: `mkdir new_folder`

5\. `**rm**` - Remove: Delete files or directories.  
Example: `rm file.txt`

6\. `**cp**` - Copy: Copy files or directories.  
Example: `cp file.txt /backup`

7\. `**mv**` - Move: Move files or directories.  
Example: `mv file.txt /new_location`

8\. `**touch**` - Create Empty File: Create a new empty file.  
Example: `touch new_file.txt`

9\. `**cat**` - Concatenate and Display: View the content of a file.  
Example: `cat file.txt`

10\. `**nano**` - Text Editor: Open a text file for editing.  
Example: `nano file.txt`

11\. `**grep**` - Search Text: Search for text patterns in files.  
Example: `grep "pattern" file.txt`

12\. `**find**` - Search Files and Directories: Search for files and directories. Example: `find /path/to/search -name "file_name"`

13\. `**chmod**` - Change File Permissions: Modify file permissions.  
Example: `chmod 755 file.sh`

14\. `**chown**` - Change Ownership: Change the owner and group of a file or directory.  
Example: `chown user:group file.txt`

15\. `**ps**` - Process Status: Display running processes.  
Example: `ps aux`

16\. `**top**` - Monitor System Activity: Monitor system processes in real-time. Example: `top`

17\. `**kill**` - Terminate Processes: Terminate a process using its ID.  
Example: `kill PID`

18\. `**wget**` - Download Files: Download files from the internet.  
Example: `wget [https://example.com/file.zip](https://example.com/file.zip)`

19\. `**curl**` - Transfer Data with URLs: Transfer data to or from a server. Example: `curl -O [https://example.com/file.txt](https://example.com/file.txt)`

20\. `**tar**` - Archive and Extract: Create or extract compressed archive files. Example: `tar -czvf archive.tar.gz folder`

21\. `**ssh**` - Secure Shell: Connect to a remote server securely.  
Example: `ssh user@remote_host`

22\. `**scp**` - Securely Copy Files: Copy files between local and remote systems using SSH.  
Example: `scp file.txt user@remote_host:/path`

23\. `**rsync**` - Remote Sync: Synchronize files and directories between systems.  
Example: `rsync -avz local_folder/ user@remote_host:remote_folder/`

24\. `**df**` - Disk Free Space: Display disk space usage.  
Example: `df -h`

25\. `**du**` - Disk Usage: Show the size of files and directories.  
Example: `du -sh /path/to/directory`

26\. `**ifconfig**` - Network Configuration: Display or configure network interfaces (deprecated, use `ip`).  
Example: `ifconfig`

27\. `**ip**` - IP Configuration: Manage IP addresses and network settings. Example: `ip addr show`

28\. `**netstat**` - Network Statistics: Display network connections and statistics (deprecated, use `ss`).  
Example: `netstat -tuln`

29\. `**systemctl**` - System Control: Manage system services using systemd. Example: `systemctl start service_name`

30\. `**journalctl**` - Systemd Journal: View system logs using systemd's journal.  
Example: `journalctl -u service_name`

31\. `**free**` - This command displays the total amount of free space available.  
Example: `free -m`

32\. `**at**` - Execute Commands Later: Run commands at a specified time. Example: `echo "command" | at 15:30`

33\. `**ping**` - Network Connectivity: Check network connectivity to a host. Example: `ping google.com`

34\. `**traceroute**` - Trace Route: Trace the route packets take to reach a host. Example: `traceroute google.com`

35\. `**curl**` - Check Website Connectivity: Check if a website is up.  
Example: `curl -Is https://example.com | head -n 1`

36\. `**dig**` - Domain Information Groper: Retrieve DNS information for a domain.  
Example: `dig example.com`

37\. `**hostname**` - Display or Set Hostname: Display or change the system's hostname.  
Example: `hostname`

38\. `**who**` - Display Users: Display currently logged-in users.  
Example: `who`

39\. `useradd` - Add User: Create a new user account.  
Example: `useradd newuser`

40\. `**usermod**` - Modify User: Modify user account properties.  
Example: `usermod -aG groupname username`

41\. `**passwd**` - Change Password: Change user password.  
Example: `passwd username`

42\. `**sudo**` - Superuser Do: Execute commands as the superuser.  
Example: `sudo command`

43\. `**lsof**` - List Open Files: List open files and processes using them. Example: `lsof -i :port`

44\. `**nc**` - Netcat: Networking utility to read and write data across network connections.  
Example: `echo "Hello" | nc host port`

45\. `**scp**` - Secure Copy Between Hosts: Copy files securely between hosts. Example: `scp file.txt user@remote_host:/path`

46\. `**sed**` - Stream Editor: Text manipulation using regex.  
Example: `sed 's/old/new/g' file.txt`

47\. `**awk**` - Text Processing: Pattern scanning and text processing.  
Example: `awk '{print $2}' file.txt`

48\. `**cut**` - Text Column Extraction: Extract specific columns from text. Example: `cut -d"," -f2 file.csv`

49\. `**sort**` - Sort Lines: Sort lines of text files.  
Example: `sort file.txt`

50\. `**diff**` - File Comparison: Compare two files and show differences. Example: `diff file1.txt file2.txt`

51\. `**ls**` - List Files and Directories: List the contents of a directory.  
Example: `ls -la`

52\. `**history**` - This command is used to view the previously executed command.  
Example: `history 10`

53\. `**cron**` - Schedule Tasks: Manage scheduled tasks.  
Example: `crontab -e`

54\. `**ssh-keygen**` - This command is used to generate a public/private authentication key pair. This process of authentication allows the user to connect remote server without providing a password.  
Example: `ssh-keygen`

55\. `**nslookup**` - This stands for “Name server Lookup”. This is a tool for checking DNS hostname to Ip or Ip to Hostname. This is very helpful while troubleshooting.  
Example: `nslookup google.com`

56\. `**tr**` - For translating or deleting characters.

These commands cover a wide range of tasks that are essential for DevOps professionals working with Linux systems. Remember to always refer to the man pages (`man command`) for more detailed information about each command and its options.  
Example:`cat crazy.txt | tr "[a-z]" "[A-Z]"`

57\. `**tnc**` - This is “Test Network Connection” command. Mostly used command while troubleshooting. It displays diagnostic information for a connection.  
Example:`tnc google.com --port 443`

58\. `**w**` \- Displays current user.

59\. `**su**` **-** Switch User.  
Example: `su - root`

60\. `**ac(All Connections)**` **—** Total connect time for all users or specified users.  
Example: `ac john`
