# Exercise 17.23

Give the commands necessary to automate the earlier script file using cron, to run the backup.sh script at 3:00 A.M. every week. Feel free to modify time, day, and source and destination directories and files, so that you can use the script file to backup information important to you on your Linux system.

# 17.6.3.3 Software for Backup and Recovery: The “Zillas” and Ghost

There are many commercial software and hardware packages that can be deployed to backup and archive your system. One very easy-to-use commercial product that allows you to clone entire hard disks in a “broadcast” fashion over a network, from a server to one or more machines, is Norton Ghost. But the two most readily available, useful, and free software facilities that can do a variety of file system backup and recovery, disk recovery, and disk cloning operations are FileZilla and Clonezilla.

# 17.6.3.3.1 FileZilla

FileZilla is nominally a graphics-based ftp client and server program that can use ssh as the tunnel or conduit between systems. It has a number of useful functions and menu choices that allow the system administrator to successfully, confidentially, and efficiently backup and restore single files or directories, via a network globally. It is most useful for backing up and restoring single-user files and directories.

It is not a replacement or substitute for the command line facilities shown in the preceding sections. Figure 17.10 illustrates the screen display and menus available in the “client” version of FileZilla.

![](bbox=[0.105, 0.425, 0.89, 0.9])

FIGURE 17.10 FileZilla main window.