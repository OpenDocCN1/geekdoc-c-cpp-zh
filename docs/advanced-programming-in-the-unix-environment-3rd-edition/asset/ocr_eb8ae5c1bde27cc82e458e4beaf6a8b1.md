Under System V-based systems, a similar command is ps -efj. (In an attempt to improve security, some UNIX systems don't allow us to use ps to look at any processes other than our own.) The output from ps looks like

UID PID PPID PGID SID TTY CMD
root 1 0 0 1 1 ? /sbin/init
root 2 0 0 0 ? [kthreadd]
root 3 2 0 0 ? [ksoftirqd/0]
root 6 2 0 0 ? [migration/0]
root 7 2 0 0 ? [watchdog/0]
root 21 2 0 0 ? [cpuset]
root 22 2 0 0 ? [khelper]
root 26 2 0 0 ? [sync_supers]
root 27 2 0 0 ? [bdi_default]
root 29 2 0 0 ? [kblockd]
root 35 2 0 0 ? [kswapd0]
root 49 2 0 0 ? [scsi_eh_0]
root 256 2 0 0 ? [jbd2/sda5-8]
root 257 2 0 0 ? [ext4-dio-unwrit]
 syslog 847 1 843 843 ? rsyslogd -c5
root 906 1 906 906 ? /usr/sbin/cupsd -F
root 1037 1 1037 1037 ? /usr/sbin/inetd
root 1067 1 1067 1067 ? cron
daemon 1068 1 1068 1068 ? atd
root 8196 1 8196 8196 ? /usr/sbin/sshd -D
root 13047 2 0 0 ? [kworker/1:0]
root 14596 2 0 0 ? [flush-8:0]
root 26464 1 26464 26464 ? rpcbind -w
statd 28490 1 28490 28490 ? rpc.statd -L
root 28553 2 0 0 ? [rpciod]
root 28554 2 0 0 ? [nfsiod]
root 28561 1 28561 28561 ? rpc.idmapd
root 28761 2 0 0 ? [lockd]
root 28764 2 0 0 ? [nfsd]
root 28775 1 28775 28775 ? /usr/sbin/rpc.mountd --manage-gids

We have removed a few columns that don't interest us, such as the accumulated CPU time. The column headings, in order, are the user ID, process ID, parent process ID, process group ID, session ID, terminal name, and command string.

> The system that this ps command was run on (Linux 3.2.0) supports the notion of a session ID, which we mentioned with the setsid function in Section 9.5. The session ID is simply the process ID of the session leader. Some BSD-based systems, such as Mac OS X 10.6.8, will print the address of the session structure corresponding to the process group that the process belongs to (Section 9.11) instead of the session ID.

The system processes you see will depend on the operating system implementation. Anything with a parent process ID of 0 is usually a kernel process started as part of the system bootstrap procedure. (An exception is init, which is a user-level command started by the kernel at boot time.) Kernel processes are special and generally exist for the entire lifetime of the system. They run with superuser privileges and have no controlling terminal and no command line.