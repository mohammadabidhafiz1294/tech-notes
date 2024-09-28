## Definition
**FileSystem**, also known as #FileSystem  or **fs**, is a method and data structure that the operating system uses to control how data is stored and retrieved. By separating the data into pieces and giving each a name, the data is easily isolated and identified. Taking its name from the way a paper-based data management system is named, each group of data is called a 'file'. The structure and logic rules used to name the groups of data and their names is called a 'file system'.

### Why Is File System Important

The file system helps the operating system to manage data and files in a logical way. With it, users can easily access, secure, read, write, and modify data on their storage devices. 

Instead, without the file system, data on a drive will be stored disorderly, taking huge storage devices and making it difficult for users to access and find desired files. The file system also makes lost files easy to be retrieved.

### What's The Relationship Between File System and Operating System

If you want to understand the relationship between the file system and operating system, it's essential to learn:

**How the file system works**

A file system indexes all the data information on a storage device, including the size of the File, attributes, location, and hierarchy in the directory. The file system also specifies the path to a file via the structure of directories with a format.

![File Sytem Work Flow](https://www.easeus.com/images/en/screenshot/partition-manager/file-system-work-flow.png)

**Structure of file system metadata**

All the data information of files on a storage drive is stored in the file system metadata:

-   Date created
-   Date modified
-   Last date of access
-   Last backup
-   User ID of the file creator
-   Access permissions
-   File size

**How the operating system access file system**

![File System and operating system](https://www.easeus.com/images/en/screenshot/partition-manager/file-system-and-operting-system.png)

Here is how the operating system uses the file system to process and access files on a storage device:

-   You create a partition on a hard drive or external drive.
-   You add a file system format to the drive.
-   You store a file in a folder, a directory, or a subdirectory on the drive. 
-   The file system record the location information of these files.
-   OS uses the file system to store and locate these files on your storage devices.

Check the image here, and you'll get the relationship between the file system and OS:

### Types of File System Format

When it comes to learning the types of file systems, there are more than 10 types of file systems. They are disk file systems, flash file systems, tape file systems, database file systems, transactional file systems, network file systems, shared-disk file systems, special file systems, minimal file systems, and flat file systems.

They all are not like the ones you already know, right? When we mention the NTFS, FAT32, or HFS file system, we are talking about the file system format of disk drives. You can also take it as disk file system formats. 

Here is a list of popular file system formats that are used on Windows, Mac, and Linux operating systems: 

-   **Windows File System** - FAT, NTFS, exFAT
-   **macOS** - HFS, APFS, HFS+
-   **Linux** - EXT2/3/4, XFS, JFS, Btrfs

## File System Format: NTFS, FAT32, exFAT, or EXT2/3/4, Which Should I Use

So what is the best file system format on Windows? NTFS, FAT32, exFAT, or EXT? Which should I use? We'll thoroughly discuss these 3 questions here in this part. So follow and get to learn when to use the correct file system format on your drive now.

### What Is NTFS, FAT32, exFAT, and EXT2/3/4 File System

First, let's get a basic idea about NTFS, FAT32, exFAT, and EXT2/3/4. 

**1. NTFS File System**

NTFS, also called New Technology File System, is a proprietary journaling file system developed by Microsoft. Starting with Windows NT 3.1, it is the default file system of the Windows NT family. It superseded File Allocation Table (FAT) as the preferred file system on Windows and is also supported in Linux and BSD. - by [Wikipedia](https://en.wikipedia.org/wiki/NTFS)

The [NTFS file system](https://www.easeus.com/partition-manager-software/ntfs-file-system.html) is regarded as the default file system format in Windows operating systems, and it surpassed the FAT file system in some ways. Check the list below and learn more about it:

-   **Initial Release:** 1993
-   **Developer:** Tom Miller, Gary Kimura, Brain Andrew, and David Goebel.
-   **Last Version:** V3.1, (Commonly called NTFS 5.1)

NTFS File System Structure: 

The NTFS file system has 5 components: O Boot Record， MFT1, MFT Metadata, MFT2, and Data Area.

![Structure of NTFS file system](https://www.easeus.com/images/en/screenshot/partition-manager/ntfs-file-system-structure.png)

Learn More About NTFS:

Follow this link: [What Is NTFS File System, Do I Need It](https://www.easeus.com/partition-manager-software/ntfs-file-system.html), and learn more details about the NTFS file system format. 

**2. FAT or FAT32**

FAT, also known as File Allocation Table, is a file system developed for personal computers. Originally developed in 1977 for use on floppy disks, it was adapted for use on hard disks and other devices. It is often supported for compatibility reasons by current operating systems for personal computers and many mobile devices and embedded systems, allowing the interchange of data between disparate systems. - by [Wikipedia](https://en.wikipedia.org/wiki/File_Allocation_Table)

According to Wikipedia, FAT32, a successor of FAT16, was designed by Microsoft as a new file system version. FAT32 supports an increased number of possible clusters and reuses most of the existing codes. This file system overcomes the volume size limit of FAT16 and allows DOS real-mode code to handle the format. 

-   **Initial Release:** 1977
-   **Developer:** Microsoft, NCR, IBM, Caldera, and more.
-   **Last Version:** FAT32

FAT File System Structure:

The FAT file system consists of four major components: Reserved sectors, FAT Region, Root Directory Region, and Data Region.

![FAT file system structure](https://www.easeus.com/images/en/screenshot/partition-manager/fat-file-system-structure.png)

**3. exFAT File System**

exFAT, also called Extensible File Allocation Table, is a file system introduced by Microsoft in 2006 and optimized for flash memory such as USB flash drives and SD cards. exFAT was proprietary until 28 August 2019, when Microsoft published its specification. - by [Wikipedia](https://en.wikipedia.org/wiki/ExFAT). 

According to Wikipedia, it's clear that the exFAT file system is a new format that is primarily designed for removable storage devices, like USB flash drives, SD cards, etc.

-   **Initial Release:** 2006
-   **Developer:** Microsoft
-   **Last Version:** exFAT

exFAT File System Structure:

The exFAT file system consists of 4 main sections: the Main Boot Region, Backup Boot Region, FAT Region, and Data Region.

![exFAT file system Structure](https://www.easeus.com/images/en/screenshot/partition-manager/exfat-file-system-structure.png)

Learn More About exFAT:

What is the exFAT file system designed for? Click here to learn about [What Is exFat Format: Everything You Need to Know](https://www.easeus.com/partition-manager-software/what-is-exfat-format.html).

**4. EXT File System - EXT2/3/4**

EXT, known as the extended file system, was implemented in April 1992 as the first file system created specifically for the Linux kernel. It has a metadata structure inspired by traditional Unix file system principles and was designed by Remy Card to overcome certain limitations of the MINIX file system. - by [Wikipedia](https://en.wikipedia.org/wiki/Extended_file_system)

According to Wikipedia, it's clear that the EXT file system is a Linux format that takes the place of the MINIX file system.

-   **Initial Release: 1992**
-   **Developer:** Remy Card
-   **Last Version:** EXT4

EXT File System Structure:

The EXT file system can be divided into one block and two groups, including the Boot Block, Block Group 0 (which contains Super Block, Group Descriptors, Data Block Bitmap, Inode Bitmap, Inode Table, and Data Blocks), and Block Group n.

![ext file system structure](https://www.easeus.com/images/en/screenshot/partition-manager/ext-file-system-structure.png)

### NTFS VS FAT32 VS exFAT VS EXT2/3/4, What's The Difference

So what's the difference between NTFS, FAT32, exFAT, and EXT/2/3/4 file systems? The biggest difference is that these file system formats are designed for different circumstances and purposes.

**Comparison: NTFS VS FAT32, FAT32 VS exFAT, exFAT VS EXT2/3/4**

Here we compared NTFS, FAT32, exFAT, and EXT2/3/4 and listed all differences here in this table. Check the differences here now:

Differences

Max File Size

Max Volume Size

Operating System

NTFS

-   16EB - 1KB
-   16TB - 64KB
-   256TB - 64KB
-   8PB - 2MB

-   256TB - 64KB
-   8PB - 2MB

-   Windows NT3.1 and later
-   macOS X 10.3 and later (Read-only)
-   Linux kernel 2.6 and later (read-only)
-   FreeBSD, NetBSD, OpenBSD(read-only), Chrome OS, Solaris, ReactOS(read-only)

FAT32

-   4GB

-   2TB - 512 byte
-   8TB - 2KB
-   16TB - 4KB

-   Windows 95OSR2, Windows 98, XP, 7, 8, 10, and 11.
-   macOS 
-   Linux

exFAT

-   128 #PB

-   128 PB

-   Windows XP, Vista, 1/8/10/11, Windows Server 2003/2008/2008 R2
-   Linux kernal 5.4 and later, FUSE
-   Mac OS X 6.5 and later

EXT2/3/4

-   4TB - 1KB
-   8TB - 2KB
-   16TB - 4KB
-   256PB - 64KB

-   4TB - 1KB
-   8TB - 2KB
-   16TB - 4KB
-   256PB - 64K

-   Linux kernel 0.96 and later

According to this table, it's clear that different operating systems respectively support each file system. Also, the maximum file size and maximum volume size are different.

If you are wondering about more differences between these file systems, click the links here to get more details: [NTFS vs. exFAT vs. FAT32](https://www.easeus.com/partition-master/fat32-exfat-or-ntfs.html), NTFS or FAT32, Best File System for USB

### Which File System Should I Use, NTFS, FAT32, exFAT, or EXT?

So when do I use NTFS, exFAT, or FAT32? We compared these file system formats together and came out with the listed suggestions for you.

Here is when to use the right file system:

**On Windows -**

-   NTFS - Set for the OS or data drive, huge file storage or transfer (bigger than 4GB), or use it on a gaming disk.
-   Fat32 - Set for external gaming drive, Android memory card, small-capacity USB or SD card (32GB or smaller).
-   exFAT - Super huge file storage (8K videos) for a big external hard drive (64GB or bigger)

**On macOS -**

-   APFS - macOS 10.13-10.15, external SSD
-   HFS+ - Mac OS X (pre-2-16), Time Machine backup, Mechanical hard drive
-   Extend File Allocation Table (exFAT) - Use both on Mac and Windows, external hard drive
-   MS-DOS (FAT32) - USB flash drive, save individual files less than 4GB on USB.

**On Linux-** 

-   EXT4 is regarded as the best Linux file system for now.


#PB :  A petabyte (PB) is a unit of digital information storage that represents 1,000,000,000,000,000 bytes, or 10^15 bytes. It is a very large amount of data storage.
	To give you an idea of scale, a petabyte is larger than a terabyte (10^12 bytes), a gigabyte (10^9 bytes), and a megabyte (10^6 bytes). It is often used to measure data storage in large-scale systems, such as data centers or 
	enterprise-level storage solutions.
	128 PB is an enormous amount of storage capacity and is typically associated with highly demanding applications like big data analytics, scientific research, or cloud storage services. It can hold a massive volume of data, including files, documents, images, videos, and more.



### L.V.M. (Logical #Volume-Manager ):
 
 L.V.M. provides logical volume management, which allows for more flexible and dynamic management of storage. With LVM, you can create logical volumes that span multiple physical disks, resize volumes on the fly, and create snapshots for backups. This flexibility is useful in scenarios where you need to efficiently manage and allocate storage resources across multiple disks or when you want to resize or reorganize storage without disrupting the file system. LVM allows for easier volume management and increases the overall flexibility of storage configuration.
 
 
### BTRFS (B-tree #FileSystem):

 Btrfs is a modern, next-generation file system designed to address limitations of earlier file systems like ext4. It introduces several advanced features, including built-in RAID support, snapshot capabilities, subvolumes (isolated file system trees within a single file system), and data checksumming for enhanced data integrity. Btrfs aims to provide improved scalability, performance, and data protection compared to traditional file systems. It also supports features like transparent compression, online file system repair, and online resizing. Btrfs is particularly useful in scenarios where you require advanced data management capabilities or want to experiment with new file system technologies.

 

 
