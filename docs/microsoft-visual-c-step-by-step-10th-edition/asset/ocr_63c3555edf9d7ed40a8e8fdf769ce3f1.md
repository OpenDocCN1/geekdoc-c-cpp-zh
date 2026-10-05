| To | Do this |

Provide exclusive write access to a resource but shared read access

Use a `ReaderWriterLockSlim` object. Before reading the shared resource, call the `EnterReadLock` method. Call the `ExitReadLock` method when you've finished. Before writing to the shared resource, call the `EnterWriteLock` method. Call the `ExitWriteLock` method when you've completed the write operation. For example:

Click here to view code image

```
ReaderWriterLockSlim readerWriterLock = new ReaderWriterLockSlim();

Task readerTask = Task.Factory.StartNew(() => {
    readerWriterLock.EnterReadLock();
    // Read shared resource
    readerWriterLock.ExitReadLock();
});

Task writerTask = Task.Factory.StartNew(() => {
    readerWriterLock.EnterWriteLock();
    // Write to shared resource
    readerWriterLock.ExitWriteLock();
});
```