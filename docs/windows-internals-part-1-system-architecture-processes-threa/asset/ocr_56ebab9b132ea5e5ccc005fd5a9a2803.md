# Stage 3E: Setting up the PEB

NtCreateProcess calls MiCreatePeb, which maps the system-wide National Language Support (NLS) tables into the process's address space. It calls MiCreatePebOr to allocate a page for the PEB and initializes a number of fields, most based on internal variables that are configured through the registry, such as MinHeap* values, MiCriticalSectionTimeout, and MinStackCommitInBytes. Some of these fields can be overridden by settings in the linked executable image, such as the Windows version in the PE header or the affinity mask in the load configuration of the PE header.

If image header characteristics IMAGE_FILE_SYS_ONLY flag is set (indicating that the image can run only on a uniprocessor system, a CmpRtlProcessorNumber is chosen for all the threads in this new process to run on). The selection process is performed by simply cycling through the available processors. Each time this type of image is run, the next processor is used. In this way, these types of images are spread evenly across the processors.

# Stage 3F: Completing the setup of the executive process

Before the handle to the new process can be returned, a few setup steps must be completed, which are performed by PsInsertProcess and its helper functions:

+   If system-wide auditing of processes is enabled (because of either local policy settings or group policy from a domain controller), the process's creation is written to the Security event log.

+   If the parent process was contained in a job, the job is recovered from the job level of the parent and bound to the session of the newly created process. Finally, the new process is added to the job.

+   The new process is inserted at the end of the Windows list of active processes (PsActive-ProcessHead). Now the process is accessible via functions like EnumProcesses and OpenProcess.

+   The process debug flag of the parent process is copied to the new process unless NoDebugFlag is set (which can be requested when creating the process). If a debug port was specified, it is attached to the new process.

+   Job objects can specify restrictions on which group or groups the threads within the processes of a job can run on. Therefore, PsInsertProcess must make sure the affinity associated with the process would not violate the group affinity associated with the job. An interest-secondary issue to consider is if the job's permissions grant access to modify the process's affinity permissions, because a less-privileged job object might interfere with the more privileged process.

+   Finally, PsInsertProcess creates a handle for the new process by calling ObOpenObjectByPointer, and then returns this to the caller. Note that no process-creation callback is sent until the first thread within the process is created, and the code sends process callbacks before sending object managed-based callbacks.