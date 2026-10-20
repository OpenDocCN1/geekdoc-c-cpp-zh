15. Give the command for deleting the memos directory. How do you know that the directory has been deleted?

16. What is the purpose of the following command? What happens when you run this command on your Linux system? Does the command output make sense? Explain your answer.

rmdir -p ~/personal/diary

17. Why does a shell process terminate when you press <Ctrl+D> at the beginning of a new line?

18. Give a command to display the types of all the files in your ~/linux2e directory that start with the word chapter, are followed by one of the digits 1, 2, 6, 8, or 9, and end with .eps or .prn.

19. Give a command line to display the types of all the files in the personal directory in your home directory that do not start with letters a, k, G, or Q and the third letter in the name is not a digit and not a letter (uppercase or lowercase).

20. Use the ls -i command to display inode numbers for the /, /usr, and ~ directories on your system. Show outputs of your commands and identify the inode numbers for these directories.

21. What are ELF and core dump?

22. Where are the permissions and most other attributes for a file stored in Linux?

23. Display the absolute pathnames of your home directory by using two different methods in the Bash and TC shells. Does your system use any symbolic links in the / directory? If so, display those symbolic links by using a shell command.

24. Discuss possible ways to create files on Linux. Use the fallocate command to create files of sizes 20 and 200 GB.

25. What is a file descriptor in Linux? What are standard files? What are their descriptors?

26. What is the concept of redirection of standard files?

27. Why do you think the system-wide file table is required between the per process file descriptor table and the inode table?

28. What are sector, track, platter, and cylinder? What is the size of a sector in hard disks these days?

29. What are block and cluster?

30. What are the basic characteristics of the ZFS file system? After referring to Chapter W22 and the online resource for ZFS, is ZFS integrated into the Linux kernel, or is it a kernel-loadable module?

31. What is the maximum size (in bytes/characters) of the file name in your Linux system? What command did you use to obtain your answer?

32. Browse through the following directories and identify five commonly used commands, tools, utilities, and daemons in them: /bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin, and /usr/local/sbin. Clearly state the purpose of each command, tool, utility, or daemon and the name of the directory in which it is found.

33. We say that Ext4 is backward compatible. What does it mean?

34. What size volumes and files does Ext4 support? How many directories may be created on the Ext4 file system?

35. Repeat Question 26 for ZFS and XFS.

36. How many file systems are mounted on your system? How many of these are of type Ext4, XFS, ZFS, and cgroups type each? Show the commands you used to obtain your answers.

37. How many file systems each are mounted under /sys and /dev on your system. Show the command you use to obtain your answer along with the output of the command.

38. How many files can a directory have under ZFS? Please give number in trillion.