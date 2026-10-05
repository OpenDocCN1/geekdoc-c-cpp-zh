# Page files

Page files store modified pages that are still in use by some process but had to be written to disk because they were unmapped or memory pressure resulted in a tran. Page file space is reserved when the pages are initially committed, but the actual clustered page file locations change until the pages are written to disk.

When the system boots, the Session Manager (Smss.exe) reads the list of page files to open by examining the HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory\PagingFiles registry. This registry value contains the name, minimum, and size of each page file window. Windows supports up to 16 paging files on x86 and x64 and up to 2 paging files on ARM. Once open, the page files can't be deleted while the system is running because the System process maintains an open handle to each page file.

Because the page file contains parts of process and kernel virtual memory, for security reasons, the system can be configured to clear the page file at shutdown. To enable this, set the ClearPageF1AtShutdown registry value in HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory key to 1. Otherwise, after shutdown, the page file will contain whatever happened to have been paged out while the system was up. This data could be accessed by someone who gained physical access to the machine.

If the minimum and maximum page file sizes are both zero (or not specified), this indicates a system-managed paging file. Windows 7 and Server 2008 R2 used a simple scheme based on RAM as follows:

+   - Minimum size Set to the amount of RAM or 1 GB, whichever is larger

+   - Maximum size Set to 3 * RAM or 4 GB, whichever is larger

These settings are not ideal. For example, today's laptops and desktop machines can easily have 32 GB or 64 GB of RAM, and server machines can have hundreds of gigabytes of RAM. Setting the initial page file to the size of RAM may result in a considerable loss of disk space, especially if disks are relatively small and based on solid-state drive (SSD). Furthermore, the amount of RAM in a system is not necessarily indicative of the typical workload working on that system.

The current implementation uses a more elaborate scheme to derive a 'good' minimum page file size not only on RAM size, but also on page file history and other factors. As part of page file creation and initialization, Smss.exe calculates page file minimum sizes based on four factors, stored in global variables:

+   - RAM (SmpDesiredFileSizeBasedOnRAM) This is the recommended page file size based on RAM.

+   - Crash dump (SmpDesiredPfSizeForCrashDump) This is the recommended page file size needed to be able to create a crash dump.

+   - History (SmpDesiredPfSizeBasedOnHistory) This is the recommended page file size based on usage history. Smss.exe uses a timer that triggers once an hour and records the page file usage.