tempfile. We have to use the df command in this example to see the actual amount of free space on the file system.

# 4.9

If the link being removed is not the last link to the file, the file is not removed. In this case, the changed-status time of the file is updated. But if the link being removed is the last link to the file, it makes no sense to update this time, because all the information about the file (the i-node) is removed with the file.

# 4.10

We recursively call our function dopath after opening a directory with opendir. Assuming that opendir uses a single file descriptor, this means that each time we descend one level, we use another descriptor. (We assume that the descriptor isn’t closed until we’re finished with a directory and call closedir.) This limits the depth of the file system tree that we can traverse to the maximum number of open descriptors for the process. Note that the nftw function as specified in the XSI option of the Single UNIX Specification allows the caller to specify the number of descriptors to use, implying that it can close and reuse descriptors.

# 4.12

The chroot function is used by the Internet File Transfer Protocol (FTP) program to aid in security. Users without accounts on a system (termed anonymous FTP) are placed in a separate directory, and a chroot is done to that directory. This prevents the user from accessing any file outside this new root directory.

In addition, chroot can be used to build a copy of a file system hierarchy at a new location and then modify this new copy without changing the original file system. This could be used, for example, to test the installation of new software packages.

Only the superuser can execute chroot, and once you change the root of a process, it (and all its descendants) can never get back to the original root.

# 4.13

First, call stat to fetch the three times for the file; then call utime to set the desired value. The value that we don’t want to change in the call to utime should be the corresponding value from stat.

# 4.14

The finger(1) command calls stat on the mailbox. The last-modification time is the time that mail was last received, and the last-access time is when the mail was last read.

# 4.15

Both cpio and tar store only the modification time (st_mtime) in the archive. The access time isn’t stored, because its value corresponds to the time the archive was created, since the file has to be read to be archived. The -a option to cpio has it reset the access time of each input file after the file has been read. This way, the creation of the archive doesn’t change the access time. (Resetting the access time, however, does modify the changed-status time.) The changed-status time isn’t stored in the archive, because we can’t set this value on extraction even if it was archived. (The utimes function and its related functions, futimens and utimensat, can change only the access time and the modification time.)

When the archive is read back (extracted), tar, by default, restores the modification time to the value in the archive. The m option to tar tells it to not