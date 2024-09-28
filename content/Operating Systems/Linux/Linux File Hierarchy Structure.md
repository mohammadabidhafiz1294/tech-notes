## Introduction

The Linux File Hierarchy Structure or the Filesystem Hierarchy Standard (FHS) defines the directory structure and directory contents in Unix-like operating systems. It is maintained by the Linux Foundation.It’ll be using the term Linux hereafter instead of UNIX though

-   In the FHS, all files and directories appear under the root directory /, even if they are stored on different physical or virtual devices.
-   Some of these directories only exist on a particular system if certain subsystems, such as the X Window System, are installed.
-   Most of these directories exist in all UNIX operating systems and are generally used in much the same way; however, the descriptions here are those used specifically for the FHS and are not considered authoritative for platforms other than Linux.

	**Is Only a hierarchy structure??**
	
	The Linux Filesystem Hierarchy Standard (FHS) is not just a structure, it is a set of guidelines that aim to ensure that all Linux distributions use a consistent and predictable [[File System - INTRO]] structure. The FHS specifies the location and purpose of important system files and directories, and helps ensure that software applications can find the resources they need in a predictable way.
	
	The FHS is important because it makes it easier for users and developers to navigate the [[File System - INTRO]] and understand where things are located. It also helps ensure that software applications and system utilities work correctly across different Linux distributions.
	
	While the FHS is not a requirement, most Linux distributions follow it closely to ensure consistency and compatibility
	

## Explaintion

![[linux system structure.jpg| 500]] 

![[linux system structure 2.png| 500]]
![[linux-system-directoies-poster.webp]]


### Directories Structures Defined:

### /bin – Binaries

The ‘/bin’ directly contains the executable files of many basic shell commands like ls, [cp](https://linuxhandbook.com/copy-directory-linux/), [cd](https://linuxhandbook.com/cd-command-examples/) etc. Mostly the programs are in binary format here and accessible by [all the users in the Linux system](https://linuxhandbook.com/linux-list-users/).

### /dev – Device Files

This directory only contains special files, including those relating to the devices. These are virtual files, not physically on the disk.

Some interesting examples of these files are:

- [/dev/null](https://linuxhandbook.com/redirect-dev-null/): can be sent to destroy any file or string
- /dev/zero: contains an infinite sequence of 0
- /dev/random: contains an infinite sequence of random values

### /etc – Configuration Files

The /etc directory contains the core configuration files of the system, use primarily by the administrator and services, such as the password file and networking files.

If you need to make changes in system configuration (for example, changing the hostname), this is where you’ll find the respective files.

### /usr – User Binaries and Program Data

in ‘/usr’ go all the executable files, libraries, source of most of the system programs. For this reason, most of the files contained therein is read­only (for the normal user)

- ‘/usr/bin’ contains basic user commands
- ‘/usr/sbin’ contains additional commands for the administrator
- ‘/usr/lib’ contains the system libraries
- ‘/usr/share’ contains documentation or common to all libraries, for example ‘/usr/share/man’ contains the text of the manpage

### /home – User Personal Data

Home directory contains personal directories for the users. The home directory contains the user data and user-specific configuration files. As a user, you’ll put your personal files, notes, programs etc in your home directory.

When you [create a user on your Linux system](https://linuxhandbook.com/useradd-vs-adduser/), it’s a general practice to create a home directory for the user. Suppose your Linux system has two users, Alice and Bob. They’ll have a home directory of their own at locations /home/alice and /home/bob.

Do note that Bob won’t have access to /home/alice and vice versa. That makes sense because only the user should have access to his/her home. You may read about [file permissions in Linux](https://linuxhandbook.com/linux-file-permissions/) to know more on this topic.

### /lib – Shared Libraries

Libraries are basically codes that can be used by the executable binaries. The /lib directory holds the libraries needed by the binaries in /bin and /sbin directories.

Libraries needed by the binaries in the /usr/bin and /usr/sbin are located in the directory /usr/lib.

### /sbin – System Binaries

This is similar to the /bin directory. The only difference is that is contains the binaries that can only be run by root or a sudo user. You can think of the ‘s’ in ‘sbin’ as super or sudo.

### /tmp – Temporary Files

As the name suggests, this directory holds temporary files. Many applications use this directory to store temporary files. Even you can use directory to store temporary files.

But do note that the contains of the /tmp directories are deleted when your system restarts. Some Linux system also delete files old files automatically so don’ store anything important here.

### /var – Variable Data Files

Var, short for variable, is where programs store runtime information like system logging, user tracking, caches, and other files that system programs create and manage.

The files stored here are NOT cleaned automatically and hence it provides a good place for system administrators to look for information about their system behavior. For example, if [you want to check the login history in your Linux system](https://linuxhandbook.com/linux-login-history/), just check the content of the file in /var/log/wtmp.

### /boot – Boot Files

The ‘/boot’ directory contains the files of the kernel and boot image, in addition to LILO and Grub. It is often advisable that the directory resides in a partition at the beginning of the disc.

### /proc – Process and Kernel Files

The ‘/proc’ directory contains the information about currently running processes and kernel parameters. The content of the proc directory is used by a number of tools to get runtime system information.

For example, if you want to [check processor information in Linux](https://linuxhandbook.com/check-cpu-info-linux/), you can simply refer to the file /proc/cpuinfo. You want to [check memory usage of your Linux system](https://linuxhandbook.com/linux-memory-usage/), just look at the content of /proc/meminfo file.

### /opt – Optional Software

Traditionally, the /opt directory is used for installing/storing the files of third-party applications that are not available from the distribution’s repository.

The normal practice is to keep the software code in opt and then link the binary file in the /bin directory so that all the users can run it.

### /root – The home Directory of the Root

There is /root directory as well and it works as the home directory of the root user. So instead of /home/root, the home of root is located at /root. Do not confuse it with the root directory (/).

### /media – Mount point for Removable Media

When you connect a removable media such as USB disk, SD card or DVD, a directory is automatically created under the /media directory for them. You can access the content of the removable media from this directory.

### /mnt – Mount Directory

This is similar to the /media directory but instead of automatically mounting the removable media, mnt is used by system administrators to manually mount a filesystem.

### /srv – Service Data

The /srv directory contains data for services provided by the system. For example, if you run a HTTP server, it’s a good practice to store the website data in the /srv directory.

I think this much information is enough for you to understand the Linux directory structure and its usage.

In the end, if you want, you can download and save this image for quick reference to the directory structure in Linux systems.