High-CPU-Utilization-in-Linux-Machine:

To see the number of threads one specific process is using you can do the following:
# ps -p 2089 -lfT 

sometimes a process (usually java based) will have a thread leak. This can cause your system to run into system limits.
Specifically one limit I have seen systems hit is the kernel.pid_max limit.

# sysctl -a | grep kernel.pid_max  
kernel.pid_max = 32768

As you can see on my system the pid_max is 32768, this means the system can only give out 32768 PID's at one time (it will rollover if pid #'s are available).

The reason threads come into play here is because each thread has a PID, and SPID number. The SPID's also take from the pid_max number.

In ps command, "-T" option enables thread views. The following command list all threads created by a process with <pid>.
# ps -T -p <pid> 

The top command can show a real-time view of individual threads. To enable thread views in the top output, invoke top with "-H" option. This will list all Linux threads. You can also toggle on or off thread view mode while top is running, by pressing 'H' key.
#TOP -H


http://jojovedder.blogspot.in/2009/01/app-server-high-cpu-or-low-threads.html

http://javaeesupportpatterns.blogspot.in/2012/02/prstat-linux-how-to-pinpoint-high-cpu.html
