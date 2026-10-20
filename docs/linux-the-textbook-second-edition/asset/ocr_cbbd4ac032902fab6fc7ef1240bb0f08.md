You can change your shell in one of two ways:

+   Method 1. Changing to a new default for every subsequent login session on your system, and
+   Method 2. Creating additional shell sessions running on top of, or concurrently with, the default shell only during the current login session.

The premise of both methods is that the shell you want to change to is available on your system. And if it isn’t, you can use the apt command shown in Section 2.8 to install it.

Method 1. To change your default shell, after you have logged on as an ordinary user, type the following command:

```
$ chsh
password for bob: www
Changing the login shell for bob
Enter the new value, or press ENTER for the default
    Login Shell [/bin/bash]: /bin/csh
$
```

As shown on our Linux Mint system, you will be prompted for the name of the shell you want to change to. You type the complete path to the location of the shell you want to change to—for example, /bin/sh to change to the Bourne shell. Consult Table 2.4 for the complete paths to common Linux shells on your system.

If this method doesn’t work on your system, consult your instructor or system administrator for more help.

Method 2. To create or run additional shells on top of your default shell, simply type the name of the shell program (see Table 2.4) on the command line whenever you want to run that shell. The following session illustrates the use of this method to change a default Bash shell, which uses the $ as the shell prompt, to a C shell, which shows the % as the shell prompt.

```
$ echo $SHELL
/bin/bash
$ csh
%
```

The first command line allows you to determine your default shell. In this case, the system shows you that the default setting is the Bash shell. The second command line allows you to run the C shell. The fourth line shows that you have been successful, because the default C shell prompt appears on your display. If the C shell was not available on your system or was inaccessible to you, you would get an error message after the third line. If your search path does not include /bin, you either have to type /bin/csh in place of csh, or include /bin in your shell’s search path and then use the csh command.

To terminate or leave this new, temporary shell and return to your default login shell, hold down <Ctrl+D> on a blank line. If this way of terminating the new shell doesn’t work, type exit on the command line and then press <Enter>. By doing so, you halt the running of the new shell, and the default shell prompt appears on your display. If you have opened a console or terminal window on your desktop, typing exit also closes this console or terminal window.

The following in-chapter exercises ask you to determine whether various shells are available on your system by using the whereis command and, for those that are available, to read the manual pages for them by using the man command.

# In-Chapter Exercises

29. Using the whereis command illustrated in Section 2.5.1, verify the locations of the various shells listed in Table 2.4. Are all these shells available on your system? Where are they located if you do not find them at the locations shown in Table 2.4?