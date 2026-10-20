If more than one section of the man pages has information on the same word and you are interested in the man page for a particular section, you can use the -S option. The following command line therefore displays the man page for the read system call and not the man page for the shell command read.

```
$ man -S2 read
```

The command man -S3 fopen fread strcmp sequentially displays man pages for three C library calls: fopen, fread, and strcmp.

Using the man command and typing the command with the -k option allows specifying a keyword that limits the search. It is equivalent to using the apropos command. The search then yields useful man page headers from all the man pages on the system that contain just the keyword reference. For example, the following session yields the on-screen output on our Linux system:

```
$ man -k passwd
chpasswd (8)          - update group passwords in batch mode
chpasswd (8)          - update passwords in batch mode
Crypt::PasswdMD5 (3pm) - Provides interoperable MD5-
                        based crypt() functions
fgetpwent_r (3)        - get passwd file entry reentrantly
getpwent_r (3)         - get passwd file entry reentrantly
gpasswd (1)            - administer /etc/group
                        and /etc/gshadow
grub-mkpasswd-pbkdf2 (1) - generate hashed password for GRUB
pam_localuser (8)      - require users to be listed
                        in /etc/passwd
passwd (1)             - change user password
passwd (lss1)          - compute password hashes
passwd (5)             - the password file
```

Output truncated...

# 2.4.6 Other Methods of Obtaining Help

To get a short description of what any particular Linux command does, you can use the whatis command. This is similar to the command man -f. The general syntax of the whatis command is as follows:

| Syntax: |
| whatis keywords |
| Purpose: Search the whatis database for abbreviated descriptions of each keyword |
| Output: Prints a one-line description of each keyword to the screen |

The following is an illustration of how to use whatis.

The output of the two commands are truncated.

```
$ whatis man
man (7)                - macros to format man pages
man (1)                - an interface to the on-line
                        reference manuals
$
```

You can also obtain short descriptions of more than one command by entering multiple arguments to the whatis command on the same command line, with spaces between each argument. The following is an illustration of this method:

```
$ whatis login set setenv
login (1)              - begin session on the system
login (3)              - write utmp and wtmp entries
setenv (3)             - change or add an environment
```