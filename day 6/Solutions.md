ASSIGNMENT 6

Q- Is kernel hardware or software?
A- Kernel means 'Core'. It is derived from corn-->cyrnel-->kernel. Now in the context of computer operating systems, then the kernel is software, a part of them, the major/complex code which acts as a bridge between applications and computer hardware resources that it also manages.



Q- What are yum repository?         
A- YUM Repositories are warehouses of Linux software (RPM package files). RPM package file is a Red Hat Package Manager file and enables quick and easy software installation on Red Hat/CentOS Linux. ... EPEL Repository Mirrors. RPMforge Repository.



Q- What is Forking process?
A- In computing, particularly in the context of the Unix operating system and its workalikes, fork is an operation whereby a process creates a copy of itself. It is usually a system call, implemented in the kernel. Fork is the primary (and historically, only) method of process creation on Unix-like operating systems.
Q- What is zombie process?
A- On Unix and Unix-like computer operating systems, a zombie process or defunct process is a process that has completed execution (via the exit system call) but still has an entry in the process table: it is a process in the "Terminated state".

Q- What is orphan process?
A- An orphan process is a computer process whose parent process has finished or terminated, though it remains running itself. In a Unix-like operating system any orphaned process will be immediately adopted by the special init system process.







Q- kill command?
A- The kill command is a command line utility to for terminating processes. It is normally a shell built-in meaning the command is called from a users shell rather than an external executable program. By default the kill command will send a TERM signal to a process allowing the process to perform any cleanup operations before shutting down. The kill command also supports sending any other signal to a process. The kill command is used primarily to terminate or restart processes.


Q- What are the various ways to send any process in background?
A- 
=> "bg" to run it in the background. 
=>"fg" moves it to the foreground.
=>you can also start a program as a background job with an "&" on the command line.
```
# myprogram &
```

=> 1. Ctrl-z
2. jobs
or alternate method which lists the PID (note the PID is not the jobnum, the job number is shell specific to the current bash session): jobs -l
3. bg %jobnum
or alternate method %jobnum & for example for the first job %1 &

=> Using the Job Control of bash to send the process into the background:
0. Run some SOMECOMMAND
1. ctrl+z to stop (pause) the program and get back to the shell
2. bg to run it in the background
3. disown -h so that the process isn't killed when the terminal closes
4. Type exit to get out of the shell because now your good to go as the operation will run in the background in it own process so its not tied to a shell

This process is the equivalent of running nohup SOMECOMMAND



Q- ?
A- 

Q- ?
A- 

Q- ?
A- 

Q- ?
A- 
