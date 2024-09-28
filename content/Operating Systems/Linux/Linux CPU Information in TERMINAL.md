To get Linux system information in the terminal for amd64 or arm64, you can use the following commands:

- **uname**

This command displays basic information about your system, including the kernel version, CPU architecture, and operating system name. To get the CPU architecture, run the following command:

```
uname -m
```

If the output is `x86_64`, then you are running an amd64 system. If the output is `arm64`, then you are running an arm64 system.

- **lscpu**

This command displays more detailed information about your CPU, including the number of cores and threads, clock speed, and instruction sets supported. To get the CPU architecture, run the following command:

```
lscpu | grep Architecture
```

The output will be a line that says `Architecture:`, followed by the CPU architecture.

- **dpkg --print-architecture** (Debian and derivatives)

This command prints the primary architecture of the machine it is run on.

- **rpm --eval '%{_arch}'** (RPM-based systems)

This command prints the current architecture name.

In addition to the CPU architecture, you may also want to know other information about your system, such as the amount of memory, disk space, and available updates. You can use the following commands to get this information:

- **free -m**

This command displays the amount of free and used memory in megabytes.

- **df -h**

This command displays the amount of free and used disk space on all mounted filesystems.

- **apt update && apt list --upgradable** (Debian and derivatives)

This command updates the package list and lists all packages that have available updates.

- **yum update && yum check-update** (RPM-based systems)

This command updates the package list and lists all packages that have available updates.

I hope this helps!