```
api-ms-win-core-firmware-11-1-0
api-ms-win-core-guard-11-1-0
api-ms-win-core-handle-11-1-0
api-ms-win-core-heap-11-1-0
api-ms-win-core-heap-11-2-0
api-ms-win-core-heap-12-1-0
api-ms-win-core-heap-obsolete-11-1-0
api-ms-win-core-interlocked-11-1-1
api-ms-win-core-interlocked-11-2-0
api-ms-win-core-io-11-1-0
api-ms-win-core-job-11-1-0
```

# Jobs

A job is aable, shareable kernel object that allows control of one or more processes as a group. A job's basic function is to allow groups of processes to be managed and manipulated as a unit. A process can be a member of any number of jobs, although the typical case is just one. A process's association with a job object cannot be broken, and all processes created by the process and its descendants are associated with the same job object (unless child processes are created with the CREATE_BREAKAWAY_FROM_JOB flag and the job itself has restricted it). The job object records basic accounting information for all processes associated with the job and for all processes that were associated with the job but have terminated.

Jobs can be associated with an I/O completion port object, which other threads might be waiting for with the Windows GetQueCompletionStatus function or by using the Thread Pool API (the native function TpAllocJobNotification). This allows interested parties (typically the job creator) to monitor for limits and events that affect the job's security, as a new process being created or process normally exiting.

Jobs play a significant role in the nature of system mechanisms, enumerated here:

+   - They manage modern apps (UWP processes), as described in more detail in Chapter 9 in Part 2. In fact, every modern app is running under a job. You can verify this with Process Explorer, described in the "Viewing the job object" experiment later in this chapter.

+   - They are used to implement Windows Container support, through a mechanism called server silo, created in this section.

+   - They are the primary way through which the Desktop Activity Moderator (DAM) manages throttling, timer freezing, and other idle-inducing behaviors for Win32 applications and services. The DAM is described in Chapter 8 in Part 2.

+   - They allow the definition and management of scheduling groups for dynamic fair-share scheduling (DFSB), which is described in Chapter 4.