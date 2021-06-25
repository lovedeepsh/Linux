ASSIGNMENT 2

TASK 1 :- How would you check:-
a) Memory used by a process (RAM)?
Ans- 5 commands to check memory used by a process :-
1. free command
2. top command
3. htop
b) Total number of open files by a process?
Ans- lsof -p (pid)
c) Running duration of a process?
Ans- ps command and ps aux command

Task 2 :- What is file descriptor?         
Ans- A file descriptor is a number that uniquely identifies an open file in a computer's operating system. It describes a data resource, and how that resource may be accessed.
When a program asks to open a file — or another data resource, like a network socket — the kernel of the operating system grants access, makes an entry in the global file table, and provides the software with the location of that entry.
The descriptor is identified by a unique non-negative integer, such as 0, 12, or 567. At least one file descriptor exists for every open file on the system.
TASK 3 :- How to kill a process :-
Ans- A process, also known as a task, is the running form of a program. Programs are stored on disk and processes run in memory. Processes have a parent/child relationship. A process can spawn one or more children. Multiple processes can run in parallel.
The process status (ps) command lists the processes that are associated with your shell.
Forcefully – kill -9  
Gracefully – kill ,  pkill







TASK 4 :-  What are signals?
Ans   :- Signal (IPC) Signals are a limited form of inter-process communication (IPC), typically used in Unix-like and other 
POSIX- compliant operating systems. A signal is an asynchronous
notification sent to a process or to a specific thread within the same process in order to notify it of an event that occured.
Linux supports both POSIX realiable signals (“hereinafter standard signals”) and Posix real-time signals.

Disposition – Each signal has a current disposition, which determines how the process behaves when it delievered the signals.
1. Term – Default action is to terminate the process.
2. IGN – Default action is to ignore the signal.
3. Core – Default action is to terminate the process and dumb core.
4. STOP – Default action is to stop the process.
5. Cont – Default action is to continue the process if it is currently stopped.

Using some system calls, a process can elect one of the behaivour to occur on delievery of the signal.
- Perform default action
- ignore the signl
- Catch the signal with a signal handler.

Signal Handler
A programmer defined function that is automatically invoked when the signal is delivered.

Sending a signal
The following system calls and library functions allow the caller to send a signal.
- raise -  send a signal to the calling thread.
- kill -  send a signal to a specified process, to all members of a specified process groups, or to all processes on the system.
- kill pg – send a signal to all of the members of a specified process groups.
- pthread_kill – sends a signal to a specified POSIX thread in the same process as the caller.
- tgkill – send a signal to a specified thread with in a specific process. This is the system calluse to impliment pthread_kill.
- sigqueue – sends a real-time signal with accompanying data to a specified process.

Standard Signals 

SIGHUP     
SIGINT
SIGQUIT
SIGILL
SIGABRT
SIGFPE
SIGKILL
SIGSEGV
SIGTERM

The signals ‘SIGKILL’ and ‘SIGSTOP’ cannot be caught, blocked or ignored. 


TASK 3 :- What is PPID?
Ans – One very important process is called INIT. 
INIT is the grandfather of all processes on the system because all other processes run under it.
Every process can be tracked back to INIT & it always has a PID of 1. The kernel itself has a PID of 0.
PPID 
In addition to unique process ID, each processes is assigned a parent process ID (PPID) that tells which process started it. The PPID is the PID of the processes parent.
For example:- If process 1 with a PID of 101 starts a processes named process 2, the process 2 will be given a unique PID, such as 3240, but it willl be given the PPID of 101.
Its a parent-child relationship. A single parent process may severel child process, each with a unique PID but all sharing the same PPID.

Why is PPID important?
Occasionally process go bad, you might try to quit a program only to find that it has other intentions.
The process might continue to run or use up resources even though its interface closed.
Sometimes, this leads to what is called a zombie process, a processes that is still running, but dead.

One effective way to kill a zombie process is to kill its parent process. This involves using the PS command to discover the PPID of the zombie process and then sending a kill signal to the parents. Ofcourse, any other children of the parent process will be killed as well.

Pstree – It is a usefull program that shows the relationship of all processes in a tree like structure.
                        

TASK 4 :- How to print a PID of the current shell?
Ans - # echo $$
         # ps -p $$


TASK 5 :- How to clear a log file of a running process?
Ans - 
1. Empty file content by redirecting to null
A easiest way to empty or blank a file content using shell redirect null to the file
```
# du -sh access.log
# > access.log
```

2. Empty file using ‘true’ command redirection
Here we will use a symbol : is a shell built-in command that is essence equilent to the ‘true’ command and it can be used as a no operation.
Another method is to redirect the output of : or true built-in command.
```
# :> access.log
```

or
```
# true > assis.log
```

3. Empty file using cat/cp/dd utilities with /dev/null
In Linux, the null device is basiclly utilized for discarding of unwanted output streams of a process or else as a suitable empty files for input streams.
This is normally done by redirection mechainism.
```
# cat /dev/null > access.log
# cp /dev/null > access.log
# dd if=/dev/null of=access.log
```

4 Empty the file using echo command
```
# echo “ “  > access.log
```

or
```
# echo > acces.log
```

or
```
# echo -n “ ” > acces.log
```

5 Empty file using truncate command
The truncate command helps to shrink or extend the size of a file to a defined size.
You can employ it with the -s option that specifies the file size. To empty a file content, use a size of 0. 
```
# truncate -s 0 access.log
```


TASK 5 :- What will happen if you delete a log file of running process?
Ans – If you will delete a log file of a running process or try to move it to some other place then the process itself will make another log file at the same place with the same memory which will result to consume double than before. 



TASK 6 :- How do you check all the running process in the system?
Ans – TOP command




TASK 7 :- What is DNAT and SNAT, Explain both with an example?
Ans - Destination NAT
Destination NAT means, we translate the destination address of a packet to make it go somewhere else instead of where it was originally addressed. For our scenario, it is:
```
# iptables -t nat -A PREROUTING -d 10.10.10.99/32 -j DNAT –to-destination 192.168.1.101
```

Now all IP packets coming to our machine’s (A) IP address of 10.10.10.99 will be rewritten and sent to 192.168.1.101 instead. This translation is transparent to the machine the connection is originating from and to machine B.
So if you connect from, say, 172.16.1.10 to 10.10.10.99, the packet will be rewritten upon reaching machine A and be sent to machine B. Machine B will see it coming from 172.16.1.10, it will have no idea that the connection was redirected by 10.10.10.99. This is important because when machine B replies, the FROM address in it’s reply will be it’s own IP address of 192.168.1.101.
This will cause a protocol error on your machine because your machine (172.16.1.10) will be expecting a reply from 10.10.10.99 and instead will receive a reply from 192.168.1.101.
To fix this, we now need to do SNAT – Source Network Address Translation.
SOURCE SNAT
We want to do SNAT to translate the from address of our reply packets to make them look like they’re coming from 10.10.10.99 instead of 192.168.1.101. To do this, we need to apply a SNAT iptables rule on a router along the path these reply packets will take. Since our machine A is the default gateway for machine B, we will do the SNAT on machine A as well.
iptables -t nat -A POSTROUTING -s 192.168.1.101/32 -j SNAT –to-source 10.10.10.99
This rewrites our source address to look like the packets are coming from 10.10.10.99 instead of 192.168.1.101.
At this point, try to connect to machine A using SSH and log in using credentials for machine B.
Once you’ve confirmed this works, you can save your iptables configuration with:
service iptables save
You can then configure iptables to run at startup automatically.
/sbin/chkconfig –level 3 iptables on
/sbin/chkconfig –level 5 iptables on
And that concludes a basic DNAT/SNAT configuration. In most situations you may want to narrow down the match criteria to specific protocols or ports. e.g. you can use the “-p tcp –dport 22” flags to match only SSH traffic.
If you’d like me to expand upon any of this further, please leave a comment asking for details.

TASK 8 :- How do you check those process that are waiting for the resources?
Ans- A. vmstat command reports information about processes, memory, paging, block IO, traps, and cpu activity. However, a real advantage of vmstat command output – is to the point and (concise) easy to read/understand. The output of vmstat command use to help identify system bottlenecks. Please note that Linux vmstat does not count itself as a running process.

```
# vmstat -S M
```

-S M: vmstat lets you choose units (k, K, m, M) default is K (1024 bytes) in the default mode. I am using M since this system has over 4 GB memory. Without -M option it will use K as unit



Task 9 :- What init process is responsible for?         
Ans- The init Process. The program init is the process with process ID 1. It is responsible for initializing the system in the required way. init is started directly by the kernel and resists signal 9, which normally kills processes.
All other programs are either started directly by init or by one of its child processes.
nit is centrally configured in the /etc/inittab file where the runlevels are defined. The file also specifies which services and daemons are available in each of the runlevels. Depending on the entries in /etc/inittab, several scripts are run by init. For reasons of clarity, these scripts, called Init scripts, all reside in the directory /etc/init.d.
The entire process of starting the system and shutting it down is maintained by init.


TASK 10 :- What are Running, Waiting, Stopped and Zombie processes?
Ans- 
Running – here it’s either running (it is the current process in the system) or it’s ready to run (it’s waiting to be assigned to one of the CPUs). 
Waiting – in this state, a process is waiting for an event to occur or for a system resource. Additionally, the kernel also differentiates between two types of waiting processes; interruptible waiting processes – can be interrupted by signals and uninterruptible waiting processes – are waiting directly on hardware conditions and cannot be interrupted by any event/signal. 
Stopped – in this state, a process has been stopped, usually by receiving a signal. For instance, a process that is being debugged. 
Zombie – here, a process is dead, it has been halted but it’s still has an entry in the process table. 

TASK 11 :-  How do you you elevate the priority of a process?
Ans   :- You can change the process priority using nice and renice utility. Nice command will launch a process with an user defined scheduling priority. Renice command will modify the scheduling priority of a running process. Linux Kernel schedules the process and allocates CPU time accordingly for each of them.But, when one of your process requires higher priority to get more CPU time, you can use nice and renice command as explained in this tutorial.
The process scheduling priority range is from -20 to 19. We call this as nice value.A nice value of -20 represents highest priority, and a nice value of 19 represent least priority for a process.By default when a process starts, it gets the default priority of 0.

1. Display Nice Value of a Process
The current priority of a process can be displayed using ps command. 
```
# perl test.pl
```

2. Launch a Program with Less Priority
Instead of launching the program with the default priority, you can use nice command to launch the process with a specific priority.
```
# nice -10 perl test.pl
```

3. Launch a Program with High Priority
You can also launch a program with a higher priority. Negative nice value will increase the priority a the process.
```
# nice --10 perl test.pl
```

4. Change the Priority with option -n
The process priority can be adjusted with the help of -n option.
```
# nice -n -5 perl test.pl
```

5. Change the Priority of a Running Process
The priority of an already running process can be changed using renice command.
```
# ps -fl -C "perl test.pl"
```

6. Change the Priority of All Processes that Belongs to a Group
Using -g option you can modify the priority of all processes that belongs to a group.
```
# renice -n 5 -g geekstuff
```


7. Change the Priority of All Processes Owned by User
Renice allows to alter the priority of all the processes owned by a specific users
```
# renice -n 5 -u bala
```

TASK 12 :- What are stdin, stdout, and stderr and how do we use them?
Ans – Linux is built being able to run instructions from the command line using switches to create the output. The question of course is how do we make use of that?
One of the ways to make use of this is by using the three special file descriptors - stdin, stdout and stderr. 
Standard input - this is the file handle that your process reads to get information from you.
Standard output - your process writes normal information to this file handle.
Standard error - your process writes error information to this file handle.

                        

TASK 13 :- How many tables are there in iptables. What filter and nat table responsible for?
Ans – There are 4 types of IP tables :-
1. Filter table
2. NAT table
3. Mangle table
4. Raw table
5. Security table

Filter Table
Filter is default table for iptables. So, if you don’t define you own table, you’ll be using filter table. Iptables’s filter table has the following built-in chains.
INPUT chain – Incoming to firewall. For packets coming to the local server. 
OUTPUT chain – Outgoing from firewall. For packets generated locally and going out of the local server. 
FORWARD chain – Packet for another NIC on the local server. For packets routed through the local server. 





NAT table
Iptable’s NAT table has the following built-in chains.
PREROUTING chain – Alters packets before routing. i.e Packet translation happens immediately after the packet comes to the system (and before routing). This helps to translate the destination ip address of the packets to something that matches the routing on the local server. This is used for DNAT (destination NAT). 
POSTROUTING chain – Alters packets after routing. i.e Packet translation happens when the packets are leaving the system. This helps to translate the source ip address of the packets to something that might match the routing on the desintation server. This is used for SNAT (source NAT). 
OUTPUT chain – NAT for locally generated packets on the firewall. 


TASK 14 :- What is the difference between -I and -A while applying a rule in iptables?
Ans – The -A option appends the rule in the end of the selected chain.

TASK 15 :- How do you check all the running process in the system?
Ans – TOP command


TASK 16 :- What is DNAT and SNAT, Explain both with an example?
Ans - Destination NAT
Destination NAT means, we translate the destination address of a packet to make it go somewhere else instead of where it was originally addressed. For our scenario, it is:
```
# iptables -t nat -A PREROUTING -d 10.10.10.99/32 -j DNAT –to-destination 192.168.1.101
```

Now all IP packets coming to our machine’s (A) IP address of 10.10.10.99 will be rewritten and sent to 192.168.1.101 instead. This translation is transparent to the machine the connection is originating from and to machine B.
So if you connect from, say, 172.16.1.10 to 10.10.10.99, the packet will be rewritten upon reaching machine A and be sent to machine B. Machine B will see it coming from 172.16.1.10, it will have no idea that the connection was redirected by 10.10.10.99. This is important because when machine B replies, the FROM address in it’s reply will be it’s own IP address of 192.168.1.101.
This will cause a protocol error on your machine because your machine (172.16.1.10) will be expecting a reply from 10.10.10.99 and instead will receive a reply from 192.168.1.101.
To fix this, we now need to do SNAT – Source Network Address Translation.
SOURCE SNAT
We want to do SNAT to translate the from address of our reply packets to make them look like they’re coming from 10.10.10.99 instead of 192.168.1.101. To do this, we need to apply a SNAT iptables rule on a router along the path these reply packets will take. Since our machine A is the default gateway for machine B, we will do the SNAT on machine A as well.
iptables -t nat -A POSTROUTING -s 192.168.1.101/32 -j SNAT –to-source 10.10.10.99
This rewrites our source address to look like the packets are coming from 10.10.10.99 instead of 192.168.1.101.
At this point, try to connect to machine A using SSH and log in using credentials for machine B.
Once you’ve confirmed this works, you can save your iptables configuration with:
service iptables save
You can then configure iptables to run at startup automatically.
/sbin/chkconfig –level 3 iptables on
/sbin/chkconfig –level 5 iptables on
And that concludes a basic DNAT/SNAT configuration. In most situations you may want to narrow down the match criteria to specific protocols or ports. e.g. you can use the “-p tcp –dport 22” flags to match only SSH traffic.
If you’d like me to expand upon any of this further, please leave a comment asking for details.

