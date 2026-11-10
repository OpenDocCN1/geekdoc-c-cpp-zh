# 2.9.5 Other Utilities

The commands that we take up in this section relate to our UNIX system. When an external command is invoked, the OS creates a *process* for it. The **ps** command shows the processes running on your terminal:

```
```text
$ ps
  PID TTY          TIME CMD
 3826 tty1     00:00:00 bash
 3990 tty1     00:00:11 vi
14367 tty1     00:00:00 ps
```
```

*The shell*

*An editing program*

*The program run to get this output*

The PID represents the process-id which is unique in the system. If a program misbehaves and you find it difficult to terminate, then you may have to use the **kill** command.

The following commands also display information related to the system:

| Command | Description |
|---|---|
| `date` | Displays system date and time. (Can be changed by administrator) |
| `uname -r` | Displays version of the operating system. |

The **passwd** command changes the user’s password. The system prompts you for the old password before it asks for the new one:

```
```text
$ passwd
Changing password for sumit.
Old Password: *******
New Password: *******
Reenter New Password: *******
Password changed
```
```

*Old and new password keyed in*

UNIX is a multi-user system and you may like to know the users currently logged on to the system like you. The output of the **who** command shows three users sharing the machine’s CPU and RAM:

```
```text
$ who
romeo      console      May  9 09:31   (:0)
henry      pts/4        May  9 09:31   (:0.0)
steve      pts/5        May  9 09:32   (saturn.heavens.com)
```
```

How does the shell locate the files representing these commands? The answer lies in the PATH variable. The shell searches the list of directories specified in PATH. This variable will always have the directories **/bin** and **/usr/bin** because they contain the external UNIX commands meant for all users:

```
```text
$ echo $PATH
/home/sumit/bin:/usr/local/bin:/usr/bin:/bin:.
```
```

**echo is an internal command**

This concludes our brief discussion on the UNIX operating system. You can try out all the commands on your Linux system if you are keen to use Linux for programming purposes. Linux is an automatic choice of course, but other considerations may lead you to choose Windows instead.