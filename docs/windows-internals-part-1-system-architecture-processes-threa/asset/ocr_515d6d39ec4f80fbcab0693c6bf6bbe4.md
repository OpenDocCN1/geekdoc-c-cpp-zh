# TABLE 6-2 File extensions

| Extension | Purpose |
| --- | --- |
| Transaction parameters | This contains the transaction parameter block, which contains information about a transacted file operation. It is returned by IogetTransactionBlock.
| Device object hint | This identifies the device object of the filter driver with which this file should be associated. It is set with IoCreateFileEx or IoFileSpecifyDeviceToObject.
| I/O status block range | This allows to lock a user-buffer into kernel-mode memory to perform asynchronous I/O. It is set with IoFileIoOverlappedRange.
| Generic | This contains filter driver-specific information, as well as extended create parameters (ECPs) created by the caller. It is set with IoCreateFileEx.
| Scheduled file I/O | This stores a file's bandwidth reservation information, which is used by the storage system to optimize and guarantee throughput for multimedia applications. (See the section "Bandwidth reservation scheduled I/O" later in this chapter) It is set with SetFileBandwidthReservation.
| Symbolic link | This is added to the file object creation when a mount point or directory junction is traversed (or a filter explicitly parses the path). It stores the caller-supplied path, including any intermediate junctions, so if a relative symbolic link is hit, it can walk back through the junctions. See Chapter 13 in Part 2 for more information on NTFS symbolic links, mount points, and directories.

When a caller opens a file or a device, the I/O manager returns a handle to a file object. Before that, the responsible driver for the device in question is asked its Create dispatch routine (IRP_MJ_CREATE) whether it's OK to open the device and allow the driver to perform any initialization request if the request is to succeed.

> Note File objects represent open instances of files, not files themselves. Unlike UNIX systems, which use inodes, Windows does not define the representation of a file; Windows file-system drivers define their own representations.

To execute objects, files are protected by a security descriptor that contains an access control list (ACL). The I/O manager consults the security subsystem to determine whether a file's ACL allows the process to access the file in the way it is requesting. If it does, the object manager grants the access and associates the granted access with the handle it returns. If this thread or another process needs to perform additional operations not specified in the original request, the thread must open the file again with a different request (or duplicate the handle with the requested access) to get another handle, which prompts another security check. (See Chapter 7 for more information about object protection).

# EXPERIMENT: Viewing device handles

Any process that has an open handle to a device will have a file object corresponding to the open instance. You can view these handles with Process Explorer by selecting a process and checking Handles in the Lower Pane View submenu of the View menu. Sort by the Type column and scroll down to see the handles that represent file objects, which are labeled as File.