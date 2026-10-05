# Modified page writer and mapped page writer

The memory manager employs two system threads to write pages back to disk and those pages back to standby lists (based on their priority). One system writes modified pages (MiModifiedPageWriter) to the paging file, and a second writes modified pages to mapped files (MiMappedPageWriter). Two threads are required to avoid creating a deadlock. This would occur if the writing of mapped files caused a page fault that in turn required a free page when no free pages were available, thus requiring the modified page writer to create more free pages. By having the modified page writer perform I/Os from a second system thread, that can wait without blocking regular page I/O.

Both threads run at priority 18, and after initialization they wait for separate event objects to trigger their operation. The mapped page writer waits on 18 event objects:

+   - An exit event, signaling the exit (not relevant to this discussion).

+   - The mapped writer event, stored in the global variable MySystemPartition.ModwriterMappedPageWriterEvent(MiMappedPageWriterEvent on Windows 8.x and Server 2012/R2). This event is signaled in the following instances:
- During a page list operation (MiInsertPageList), this routine inserts a page into one of the lists (standby, modified, etc.) based on its input arguments. Routine signals this event if the number of file-system-destined pages on the modified page list has reached more than 16 and the number of available pages has fallen below 1024.
- In an attempt to free pages (MiObtainFreePages).
- By the memory manager's working manager (MiWorkingSetManager), which runs as part of the kernel's balance manager (once every second). The working manager signals this event if the number of file-system-destined pages on the modified page list has reached more than 800.
- Upon a request to flush all modified pages (MiFlushAllPages).
- Upon a request to flush all file-system-destined pages (MiFlushAllFileSystem). In most cases, writing modified pages to their backing store files does not occur if the number of mapped pages on the modified page list is less than the maximum cluster size, which is 16 pages. This check is not made in MiFlushAllPages.

+   - An array of 16 events called ListEvent, stored in MySystemPartition.Pages.MappedPageListHead(MiMappedPageListHead on Windows 8.x and Server 2012/R2). Each time a mapped page is dirtied, it is inserted into one of these 16 page lists based on a bucket number, stored in MySystemPartition.WorkingSetControl>CurrentMappedPageBucket(MiCurrentMappedPageBucket on Windows 8.x and Server 2012/R2). This bucket number is updated by the working manager when it considers that mapped pages have gone old enough, which is currently 100 (stored in the MiWriteGapCounter variable in the same structure MiWriteGapCounter on Windows 8.x