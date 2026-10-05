+   - For device I/O control requests (IRP_MJ_DEVICE_CONTROL), each control code is constructed using the CTL_CODE macro, where some of the bits indicate the buffering method. This means the buffering method can be set on a control code-by-code basis, which is very useful.

The following sections describe each buffering method in detail.

**Buffered I/O** With buffered I/O, the I/O manager allocates a mirror buffer that is the same size as the user's buffer in non-paged pool and stores the pointer to the new buffer in the AssociatedIrp. SystemBuffer member of the IRP body. Figure 6-15 shows the main stages in buffered I/O for a read operation (write is similar).

![](bbox=[0.15, 0.24, 0.64, 0.61])

+   1 User client allocates buffer and invokes read operation
2 I/O manager allocates buffer in non-paged pool

+   3 Driver writes data to the kernel buffer
4 After the IRP completes, I/O manager copies the data to the user's buffer and frees the kernel buffer

**FIGURE 6-15 Buffered I/O.**

The driver can access the system buffer (address q in Figure 6-15) from any thread and any IRQL:

+   - The address is in system space, meaning it's valid in any process context.
- The buffer is allocated from non-paged pool, so a page fault will not happen.

For write operations, the I/O manager copies the caller's buffer data into the allocated buffer when creating the IRP. For read operations, the I/O manager copies data from the allocated buffer to the user's buffer when the IRP completes (using a special kernel APC) and frees the allocated buffer.

Buffered I/O is clearly simple to use because the I/O manager does practically everything. Its main downside is it always requires copying, which is inefficient for large buffers. Buffered I/O is commonly used when the buffer size is no larger than one page (4 KB) and when the device does not