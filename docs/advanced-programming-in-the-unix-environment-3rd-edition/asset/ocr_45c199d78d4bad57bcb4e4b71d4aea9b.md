# Example

To see the utility of the saved set-user-ID feature, let's examine the operation of a program that uses it. We'll look at the at(1) program, which we can use to schedule commands to be run at some time in the future.

On Linux 3.2.0, the at program is installed set-user-ID to user daemon. On FreeBSD 8.0, Mac OS X 10.6.8, and Solaris 10, the at program is installed set-user-ID to user root. This allows the at command to write privileged files owned by the daemon that will run the commands on behalf of the user running the at command. On Linux 3.2.0, the programs are run by the atd(8) daemon. On FreeBSD 8.0 and Solaris 10, the programs are run by the cron(1M) daemon. On Mac OS X 10.6.8, the programs are run by the launchd(8) daemon.

To prevent being tricked into running commands that we aren't allowed to run, or reading or writing files that we aren't allowed to access, the at command and the daemon that ultimately runs the commands on our behalf have to switch between sets of privileges: ours and those of the daemon. The following steps take place.

+   1. Assuming that the at program file is owned by root and has its set-user-ID bit set, when we run it, we have
+   
+   real user ID = our user ID (unchanged)
+   effective user ID = root
+   saved set-user-ID = root

+   2. The first thing the at command does is reduce its privileges so that it runs with our privileges. It calls the seteuid function to set the effective user ID to our real user ID. After this, we have
+   
+   real user ID = our user ID (unchanged)
+   effective user ID = our user ID
+   saved set-user-ID = root (unchanged)

+   3. The at program runs with our privileges until it needs to access the configuration files that control which commands are to be run and the time at which they need to run. These files are owned by the daemon that will run the commands for us. The at command calls seteuid to set the effective user ID to root. This call is allowed because the argument to seteuid equals the saved set-user-ID. (This is why we need the saved set-user-ID.) After this, we have
+   
+   real user ID = our user ID (unchanged)
+   effective user ID = root
+   saved set-user-ID = root (unchanged)
+   
+   Because the effective user ID is root, file access is allowed.

+   4. After the files are modified to record the commands to be run and the time at which they are to be run, the at command lowers its privileges by calling