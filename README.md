# BOSH-VM-System-Monitoring-Tools

BOSH VMs like the BOSH Director can be a very resource-intensive application. We need to ensure that the system running a BOSH VM like the BOSH Director has sufficient resources for things like CPU, memory, disk, and network bandwidth. If you are experiencing performance issues, there are out-of-the-box system monitoring tools like top, htop, vmstat, iostat and sar that monitor the resource utilization on the system and can help narrow down where the performance issue is coming from. We will talk briefly about each of these tools to understand its output and what it means. It's also important to note that these are just some monitoring tools that can help guide you through a performance troubleshooting exercise but they are not the only ones. There are many other helpful out-of-the-box monitoring tools like netstat or ethtool for network performance troubleshooting. I highly recommend looking at a course like "Linux Performance Monitoring & Analysis - Hands On!!" from Udemy that does a pretty good job of discussing the various monitoring tools available in a Linux operating system.

# TOP 
![Alt text](img/top.png)

Here’s how to understand this output:

+ Load average: The 3 numbers that represent the average system load over the last 1, 5, and 15 mins. A load average of 1.00 equates to 1 CPU core being 100% utilized. If you have 16 CPU cores with a load average of 8.00, that would mean that you have 8 out of 16 cores being 100% utilized or 50% usage of the total CPU for your system.
+ Tasks: This is the number of tasks running on your system broken down by the statuses of each task (running, sleeping, stopped, zombie).
+ CPU usage: The %CPU column will give you the percentage of CPU each process is using. The %MEM column will give you the percentage of memory being used by each process.
+ Memory usage: KiB Mem and KiB Swap lines will give you the total memory and swap space on your system along with the amount of free, used, and cached memory.
+ Process list: PID, USER, PR, NI, VIRT, RES, SHR, S, %CPU, %MEM, TIME+, and COMMAND columns will give you the info. on each process on your system. 
  + PID = process ID
  + USER = username of the process owner
  + PR = process priority
  + NI = nice value
  + VIRT = total virtual memory being used
  + RES = resident set size (basically, the amount of physical memory being used)
  + SHR = shared memory size
  + S = Status of the process i.e. running, sleeping, stopped, etc.
  + %CPU = percentage of CPU usage for each process
  + %MEM = percentage of memory usage for each process
  + TIME+ = total CPU time for each process
  + COMMAND = name of process

Identifying potential problems:

+ High load average: A consistently high load average may indicate that the system is under heavy load and may need additional resources or optimizations to keep up with demand.
+ High CPU usage: A process consistently using a high percentage of CPU may indicate a performance bottleneck or a runaway process. It may be necessary to investigate the cause of the high CPU usage and take steps to mitigate the issue.
+ Low memory: If the system is consistently running low on memory, it may lead to slow performance and even system crashes. It may be necessary to free up memory or add additional memory to the system.
+ Non-responsive processes: If a process is in a non-responsive or zombie state, it may indicate a problem with the system or the process itself. It may be necessary to investigate the cause of the issue and take steps to fix it.

# HTOP
![Alt text](img/htop.png)

htop is a command-line process monitoring tool and is a more advanced version of the top command. It provides real-time system monitoring by displaying a list of processes and their resource usage statistics. htop provides a more user-friendly and interactive interface than the top command.

Here’s how to understand this output:

When you run htop, it displays a list of processes that are currently running on your system. The output is organized in columns, and each column represents a specific resource usage metric. Some of the most commonly used columns include:

+ PID: This column shows the process ID number of each running process.
+ USER: This column shows the username of the user who initiated the process.
+ CPU%: This column shows the percentage of CPU resources currently being used by each process.
+ MEM%: This column shows the percentage of memory resources currently being used by each process.
+ VIRT: This column shows the virtual memory usage of each process.
+ RES: This column shows the physical memory usage of each process.
+ TIME+: This column shows the total CPU time consumed by each process.
+ COMMAND: This column shows the name of the command that is currently being executed.

htop also provides several color-coded indicators that can be helpful. The screenshot below will give you the color code and what it defines under the CPU, Memory and Swap bar.

![Alt text](img/htop_color_bar.png)

Identifying potential problems:

+ High CPU usage: If you notice that a particular process or multiple processes are consistently using a high percentage of CPU resources, it may indicate that there is a performance issue that needs to be addressed. You can use htop to identify the specific process or processes that are causing the issue and take appropriate action to optimize or terminate them.
+ High memory usage: If you notice that a particular process or multiple processes are consistently using a high percentage of memory resources, it may indicate that there is a memory leak or other performance issue that needs to be addressed. You can use htop to identify the specific process or processes that are causing the issue and take appropriate action to optimize or terminate them.
+ Processes in a state of deadlock or waiting: If you notice that a particular process or multiple processes are stuck in a state of deadlock or waiting, it may indicate that there is a problem with the system configuration or application code. You can use htop to identify the specific process or processes that are stuck and take appropriate action to resolve the issue.

# VMSTAT
![Alt text](img/vmstat.png)

vmstat displays a variety of system statistics, including CPU usage, memory usage, disk I/O, and more. 

Here’s how to understand this output:

When you run vmstat, it displays a variety of statistics that can be used to monitor system performance. The output is organized in columns, and each column represents a specific system metric. Some of the most commonly used columns include:

+ r: This column shows the number of processes that are currently waiting for CPU resources.
+ b: This column shows the number of processes that are currently blocked and waiting for I/O resources.
+ us: This column shows the percentage of CPU resources currently being used by user-level processes.
+ sy: This column shows the percentage of CPU resources currently being used by system-level processes.
+ id: This column shows the percentage of CPU resources that are currently idle.
+ wa: This column shows the percentage of CPU resources that are currently being used for I/O operations.
+ si: This column shows the amount of memory that is being swapped in from disk.
+ so: This column shows the amount of memory that is being swapped out to disk.
+ bi: This column shows the amount of data that is being read from disk.
+ bo: This column shows the amount of data that is being written to disk.

Identifying potential problems:

 + High CPU usage: If you notice that the us or sy columns are consistently showing a high percentage of CPU usage, it may indicate that there is a performance issue that needs to be addressed. 

+ High I/O wait times: If you notice that the wa column is consistently showing a high percentage of CPU usage, it may indicate that there is a problem with disk I/O performance. 

+ Memory issues: If you notice that the si or so columns are consistently showing a high amount of memory being swapped in or out from disk, it may indicate that there is a memory issue that needs to be addressed. 

# IOSTAT
![Alt text](img/iostat.png)

iostat can help you identify I/O bottlenecks, disk usage, and other performance issues. 

Here’s how to understand this output:

When you run iostat, it displays a variety of statistics that can be used to monitor I/O performance. The output is organized in columns, and each column represents a specific system metric. You'll find the more commonly used columns below:

+ Device: This column displays the name of the device being monitored.
+ %user and %system: These columns show the percentage of CPU time spent executing user-level code and kernel-level code.
+ %iowait: This column shows the percentage of time that the CPU is idle and waiting for I/O operations to complete. 
+ %steal: This column displays the percentage of CPU time that is being "stolen" by the hypervisor if the system is running in a virtualized environment.
+ %idle: This column displays the percentage of time that the CPU is idle and not executing any tasks.
+ tps: This column displays the number of I/O transactions per second.
+ kB_read/s: This column displays the amount of data read from the device in kilobytes per second.
+ kB_wrtn/s: This column displays the amount of data written to the device in kilobytes per second.
+ kB_dscd/s: This column displays the average number of kilobytes of data that's discarded by the kernel per second.
+ kB_read: This column displays the total amount of data read from the device since the system was last booted.
+ kB_wrtn: This column displays the total amount of data written to the device since the system was last booted.

Identifying potential problems:

+ If the %user or %system values are consistently high, it could indicate that the CPU is struggling to keep up with demand.
+ If the %iowait value is consistently high, it could indicate that the system is spending a lot of time waiting for I/O operations to complete.
+ If the %steal value is consistently high, it could indicate that the virtual machine is not receiving its fair share of resources and that other virtual machines on the same physical host are consuming a disproportionate amount of resources. This can lead to poor performance of the virtual machine and the applications running on it.
+ If the tps value is consistently high, it could indicate that there are too many I/O operations occurring at once, leading to poor performance.
+ If the kB_read/s and kB_wrtn/s values are consistently low, it could indicate that the disk is not performing as well as it should be.
+ If the kB_dscd/s value is consistently high, it may indicate that the system is experiencing disk I/O bottlenecks or that the disk is unable to keep up with the amount of data being written to it.

# SAR
![Alt text](img/sar.png)

The sar command also known as "System Activity Reporter" is a powerful tool that can be used to monitor system performance and identify bottlenecks. SAR collects performance data at specified intervals and stores it in log files that can be used for analysis. The SAR command can be used to monitor a variety of system resources, including CPU usage, memory usage, disk I/O, and network activity. We will focus on the SAR -r command which monitors memory utilization. Feel free to explore other useful sar command flags like the "-u" flag which will give you stats for cpu utilization. sar uses /proc filesystem for gathering information.

Here’s how to understand this output:

+ kbmemfree: The amount of free memory in kilobytes.
+ kbmemused: The amount of used memory in kilobytes.
+ kbavail: An estimate of how much memory in kilobytes is available for starting new applications, without swapping.
+ %memused: The percentage of memory used.
+ kbbuffers: The amount of memory used for buffers in kilobytes.
+ kbcached: The amount of memory used for caching file data in kilobytes.
+ kbcommit: The amount of memory in kilobytes needed for current workload. This is an estimate of how much RAM/swap is needed to guarantee that we're never out of memory.
+ %commit: A percentage of memory needed for current workload in relation to the total amount of memory (RAM+swap). This number may be greater than 100% because the kernel usually overcommits memory.
+ kbactive: Amount of active memory in kilobytes (memory that has been used more recently and usually not reclaimed unless absolutely necessary).
+ kbinact: Amount of inactive memory in kilobytes (memory which has been less recently used. It is more eligible to be reclaimed for other purposes).
+ kbdirty: Amount of memory in kilobytes waiting to get written back to the disk.

Identifying potential problems:

One of the most common problems that can be identified using the SAR -r command is high memory usage. You can spot high memory usage by checking the "%memused" column in the output. If the percentage of memory used is consistently high (over 90-95%), it may indicate that the system is running out of memory and is possibly experiencing memory pressure.

+ Identifying Memory Leaks:
Memory leaks occur when a program allocates memory but fails to release it back to the system, causing memory usage to continuously grow over time. You can spot memory leaks by monitoring the "kbmemused" column in the SAR -r output over time. If the amount of memory used continuously increases over time, it may indicate a memory leak.

+ Identifying Swapping Activity:
When a system runs out of physical memory, it may start using the swap space on the hard disk as a temporary storage area. However, swapping can significantly slow down the system. You can spot swapping activity by monitoring the "kbswpused" and "%swpused" columns in the SAR -r output. If the amount of swap space used is consistently high (over 50-60%) or if the percentage of swap space used is consistently increasing over time, it may indicate that the system is experiencing memory pressure and is swapping heavily.



