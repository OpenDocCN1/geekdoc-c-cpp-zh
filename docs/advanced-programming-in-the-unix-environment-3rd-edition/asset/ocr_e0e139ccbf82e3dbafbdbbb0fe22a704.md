If we add the line

```
set_fl(STDOUT_FILENO, O_SYNC);
```

to the beginning of the program shown in Figure 3.5, we’ll turn on the synchronous-write flag. This causes each write to wait for the data to be written to disk before returning. Normally in the UNIX System, a write only queues the data for writing; the actual disk write operation can take place sometime later. A database system is a likely candidate for using O_SYNC, so that it knows on return from a write that the data is actually on the disk, in case of an abnormal system failure.

We expect the O_SYNC flag to increase the system and clock times when the program runs. To test this, we can run the program in Figure 3.5, copying 492.6 MB of data from one file on disk to another and compare this with a version that does the same thing with the O_SYNC flag set. The results from a Linux system using the ext4 file system are shown in Figure 3.13.

| Operation | User CPU (seconds) | System CPU (seconds) | Clock time (seconds) |
|---|---|---|---|
| read time from Figure 3.6 for BUFFSIZE = 4,096 | 0.03 | 0.58 | 8.62 |
| normal write to disk file | 0.00 | 1.05 | 9.70 |
| write to disk file with O_SYNC set | 0.02 | 1.09 | 10.28 |
| write to disk followed by fdatasync | 0.02 | 1.14 | 17.93 |
| write to disk followed by fsync | 0.00 | 1.19 | 18.17 |
| write to disk with O_SYNC set followed by fsync | 0.02 | 1.15 | 17.88 |

Figure 3.13 Linux ext4 timing results using various synchronization mechanisms

The six rows in Figure 3.13 were all measured with a BUFFSIZE of 4,096 bytes. The results in Figure 3.6 were measured while reading a disk file and writing to /dev/null, so there was no disk output. The second row in Figure 3.13 corresponds to reading a disk file and writing to another disk file. This is why the first and second rows in Figure 3.13 are different. The system time increases when we write to a disk file, because the kernel now copies the data from our process and queues the data for writing by the disk driver. We expect the clock time to increase as well when we write to a disk file.

When we enable synchronous writes, the system and clock times should increase significantly. As the third row shows, the system time for writing synchronously is not much more expensive than when we used delayed writes. This implies that the Linux operating system is doing the same amount of work for delayed and synchronous writes (which is unlikely), or else the O_SYNC flag isn’t having the desired effect. In this case, the Linux operating system isn’t allowing us to set the O_SYNC flag using fcntl, instead failing without returning an error (but it would have honored the flag if we were able to specify it when the file was opened).

The clock time in the last three rows reflects the extra time needed to wait for all of the writes to be committed to disk. After writing a file synchronously, we expect that a call to fsync will have no effect. This case is supposed to be represented by the last