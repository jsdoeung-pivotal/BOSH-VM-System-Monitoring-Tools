# BOSH-VM-System-Monitoring-Tools

BOSH Director is a very resource-intensive application. We need to ensure that the system running BOSH Director has sufficient resources for things like CPU, memory, disk, and network bandwidth. If you are experiencing performance issues with the BOSH Director, there are out-of-the-box system monitoring tools like top, htop, vmstat and iostat that monitor the resource utilization on the system and can help narrow down where the performance issue is coming from. We will talk briefly about each of these tools to understand its output and what it means.

# TOP 
![Alt text](img/top.png)

Here’s how to understand this output:

+ Load average: The 3 numbers that represent the average system load over the last 1, 5, and 15 mins. A load average of 1.00 equates to 1 CPU core being 100% utilized. If you have 16 CPU cores with a load average of 8.00, that would mean that you have 8 out of 16 cores being 100% utilized or 50% usage of the total CPU for your system.
+ Tasks: This is the number of tasks running on your system broken down by the statuses of each task (running, sleeping, stopped, zombie).
+ CPU usage: The %CPU column will give you the percentage of CPU each process is using. The %MEM column will give you the percentage of memory being used by each process.
+ Memory usage: KiB Mem and KiB Swap lines will give you the total memory and swap space on your system along with the amount of free, used, and cached memory.
+ Process list: PID, USER, PR, NI, VIRT, RES, SHR, S, %CPU, %MEM, TIME+, and COMMAND columns will give you the info. on each process on your system. 
++ d 

