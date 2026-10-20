# TABLE 4.3

Some Important Hidden Files and Their Purposes

| File Name | Purpose |
|---|---|
| . | Present working directory |
| .. | Parent of the present working directory |
| .bash_history | Contains the history of commands executed under bash |
| .bashrc | Setup for the Bash shell |
| .cshrc | Setup for the C shell |
| .exrc | Setup for vi |
| .login | Setup for shell if C or tcsh shells are the login shells; executed at login time |
| .mailrc | Setup and address book for mail and mailx |
| .profile | Setup for shell if Bourne or Korn shell is the login shell; executed at login time |
| .rhosts | Domain names of the trusted hosts (see Chapter 11 for details) |
| .shrc | Setup for shell if Bourne shell is the login shell; executed at login time |
| .ssh | Keys of the servers on which you would be allowed to login using the ssh command. Keys are stored when you try to establish the session on a server for the first time |
| .vimrc | Setup for the vim text editor |
| .xsession | Customized X session script |

already discussed the . and .. directories. The purposes of some of the more important hidden files are summarized in Table 4.3.

You can also display the names of all the files and directories in a directory, including the hidden files, by using the ls command with the -a option. In the following session, the cd command places you in your home directory and the ls -a command displays all the files and directories, including the hidden files, in your home directory.

```
$ cd
$ ls -a
.           .cache      .dmrc       linux2e     Pictures    .xsession-errors
..          .config     Documents   .linuxmint  .profile
.bash_history courses     Downloads   .local      Public
.bash_logout .dbus       .ICEauthority .mozilla    Templates
.bashrc     Desktop     .lesshst    Music       Videos
$
```

You can use shell metacharacters in specifying multiple files or directory parameters to the ls command. For example, the command ls ~/courses/cs446/programs/*.c displays the names of all C program files in the ~/courses/cs446/programs directory. We discuss the use of metacharacters and regular expressions in detail later in this chapter and in Chapters 6 and 7.

You can display the sizes of files and directory sizes in human readable (K for kilo, M for mega, G for giga) form by using the -h option, as shown in the following session with the ls -sh and ls -lh commands.

```
$ ls -sh ch14
total 27G
12.6K all.tar          4.0K compute.h        4.0K main.h
8.0K analysis.txt      4.0K compute.o        4.0K main.o
9.6G bigdata           4.0K flat_profile.out  4.0K makefile
...
4.0K input.h           8.0K working           4.0K working.c
$ ls -lh all.tar analysis.txt bigdata bugged.c buggy
-rw-r--r-- 1 sarwar faculty 10K Jul 23 2017 all.tar
-rw-r--r-- 1 sarwar faculty 5.7K Oct  2 21:16 analysis.txt
```