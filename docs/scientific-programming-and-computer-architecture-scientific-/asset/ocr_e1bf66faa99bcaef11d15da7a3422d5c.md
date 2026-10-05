# Chapter 6. Special Topic: Networks and Message Passing

| nprocs | stripes | write (lsize=8MB) | read (lsize=8MB) | write (lsize=20GB) | read (lsize=20GB) |
|---|---|---|---|---||}{
| 1 | 1 | 0.5 | 0.3 | 0.2 | 0.5 |
| 10 | 10 | 0.3 | 1.3 | 1.6 | 2.3 |
| 20 | 20 | 0.6 | 2.3 | 3.3 | 4.1 |
| 50 | 50 | 1.3 | 3.2 | 6.9 | 6.2 |
| 100 | 100 | 2.6 | 6.3 | 6.6 | 7.6 |

Table 6.12: Bandwidth in GB/s on a 1 petabyte Lustre file system connected via QDR Infiniband. The reported numbers are maximums over five trials. The total size of the file divided by the number of processes (nprocs) is given as lsize.

The class definition is completed by the member function `printinfo()`.

```
void LustreFile::printinfo() {
    if(rank!=0) {
        return;
    }
    char cmd[200];
    sprintf(cmd, "ls -1 %s", dir);
    system(cmd);
    sprintf(cmd, "lfsstripe %s/%s", dir, fname);
    system(cmd);
}
```

Like `lstripe()`, `printinfo()` uses `system()` to issue commands through the shell. Table 6.12 reports bandwidth measurements on files that vary from 8 MB to 2 TB. Some of the measurements in the table, especially the ones with `lsize` of 8 MB, are probably influenced by caching. On the Lonestar cluster, the Lustre file system reaches a bandwidth of nearly 7 GB/s with 50 stripes. The cluster is used by a large number of scientists, and it is quite possible that the measurements are influenced by other jobs being run on the cluster. We do not think that likely, however. Similar numbers were obtained during measurements made on different days at different times.

Like almost all file systems, the Lustre file system also goes through a page cache on each client (for page caches see, section 4.3). The maximum size of this page cache is recorded in the file