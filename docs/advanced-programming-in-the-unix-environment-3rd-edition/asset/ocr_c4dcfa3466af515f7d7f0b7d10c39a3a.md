On Solaris, the ls command displays an 1 instead of an S to indicate that mandatory file and record locking has been enabled for this file. This behavior applies only to regular files, but we’ll discuss this more in Section 14.3.

Finally, note that the time and date listed by the ls command did not change after we ran the program in Figure 4.12. We’ll see in Section 4.19 that the chmod function updates only the time that the i-node was last changed. By default, the ls -l lists the time when the contents of the file were last modified.

The chmod functions automatically clear two of the permission bits under the following conditions:

+   - On systems, such as Solaris, that place special meaning on the sticky bit when used with regular files, if we try to set the sticky bit (S_ISVTX) on a regular file and do not have superuser privileges, the sticky bit in the mode is automatically turned off. (We describe the sticky bit in the next section.) To prevent malicious users from setting the sticky bit and adversely affecting system performance, only the superuser can set the sticky bit on a regular file.

In FreeBSD 8.0 and Solaris 10, only the superuser can set the sticky bit on a regular file. Linux 3.2.0 and Mac OS X 10.6.8 place no such restriction on the setting of the sticky bit, because the bit has no meaning when applied to regular files on these systems. Although the bit also has no meaning when applied to regular files on FreeBSD, everyone except the superuser is prevented from setting it on a regular file.

+   - The group ID of a newly created file might potentially be a group that the calling process does not belong to. Recall from Section 4.6 that it’s possible for the group ID of the new file to be the group ID of the parent directory. Specifically, if the group ID of the new file does not equal either the effective group ID of the process or one of the process’s supplementary group IDs and if the process does not have superuser privileges, then the set-group-ID bit is automatically turned off. This prevents a user from creating a set-group-ID file owned by a group that the user doesn’t belong to.

FreeBSD 8.0 fails an attempt to set the set-group-ID in this case. The other systems silently turn the bit off, but don’t fail the attempt to change the file access permissions.

FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8, and Solaris 10 add another security feature to try to prevent misuse of some of the protection bits. If a process that does not have superuser privileges writes to a file, the set-user-ID and set-group-ID bits are automatically turned off. If malicious users find a set-group-ID or a set-user-ID file they can write to, even though they can modify the file, they lose the special privileges of the file.

# 4.10 Sticky Bit

The S_ISVTX bit has an interesting history. On versions of the UNIX System that predated demand paging, this bit was known as the sticky bit. If it was set for an executable program file, then the first time the program was executed, a copy of the program’s text was saved in the swap area when the process terminated. (The text