# A.2.1.1 Files and Directories

As with the Unix/Linux environment, the folders that you are used to in a GUI are called directories on the command line, and they are used to organize files on the computer. There are a number of different commands that can be used for working with directories and files with the Windows command prompt.

+   - cd/chdir Changes the current directory.
- copy - Copy files from one location/ to another.
- del/erase - Deletes files. This does not move them to Trash like a deleter from the GUI. Once this has been executed the files cannot be recovered.
- dir - Lists the contents of the specified directory or the current directory if none is listed.
- md/mkdir - Make the specified directory.
- more - Print the contents of a file one at a time.
- move - Moves a file to a different directory.
- path - Let’s see the current path or change the path.
- ren/rename - Rename an existing file.
- rd/rmdir - Remove a specified directory.
- tree - Display the contents of a directory or drive as an ASCII based tree.

There are significant differences between directories under Windows and those under Unix/Linux. The first is that directories are separated by a backslash '\'; This is something you have to keep in mind, but it does not significantly impact how commands are used. The other difference is that Windows have different drives, each with its own directory tree.
The prompt above showed the current directory as "C:\Users\mlevis". The C: at the beginning of this specifies the drive. The drives on a Windows machine are specified as single capital letters. By default, C: is the master hard-disk of the machine. If you want to deal with locations on other drives you need to be certain to specify the drive name in the path you are using. In addition, by default the cd command will change directories or move you to a different directory. To do both you have to give the '/d' option.

# Aside

The C: standard for the hard drive arose early on. The first DOS machines did not have hard-drives. Instead, they typically had one or two floppy disk drives named A: and B:. When hard drives were added, they took the next letter in the alphabet. Even it is very rare to find a computer with a floppy drive these days, the main disk still gets the C: distinction and uses higher letters in the alphabet.
By contrast, different drives in Unix/Linux systems are represented as directories under the main directory tree that starts with /. Removable drives are mounted in subdirectories of /media.