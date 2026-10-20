The following shows how our system responded to this command when we typed it on the command line.

```
$ whoami
bob
$
```

The following in-chapter exercises give you the chance to use whereis, whoami, and two other important utility commands, who and hostname, to obtain the important information about your system.

# In-Chapter Exercises

+   21. Use the whereis command to locate binary files for the Korn shell, the Bourne shell, the Bourne again shell, the C shell, and the Z shell. Are any of these shell programs not available on your system?
+   
+   22. Use the whoami command to find your username on the system that you're using. Then use the who command to see how your username is listed, along with other users of the same system. What is the on-screen format of each user's listing that you obtained with the who command? Try to identify the information in each field in the list that you obtained with the who command?
+   
+   23. Use the hostname command to find out what host name you are logged on to. Can you determine from this list whether you are using a stand-alone computer or a networked computer system? Explain how you can know the difference from the list that the hostname command gives you.

# 2.5.2 Printing and General Utility Commands

A very useful and common task performed by every user of a computer system is the printing of text files at a printer.

This is accomplished using the configured printer(s) on the local, or a remote, system. Printers are controlled and managed with the Common UNIX Printing System. We show this utility in detail in Chapter W26, Section 5, at the book website.

The common commands that perform printing on a Linux system are lpr and lp. The general syntax of the lpr command is as follows:

Syntax:

lpr [options] filename

Purpose:

Send files to the printer

Output:

Files sent to the printer queue as print jobs

Commonly used options/features:

-P printer: Sends output to the named printer

-# copies: Produces the number of copies indicated for each named file

The following lpr command accomplishes the printing of the file named order.eps at the printer designated on our system as spr. Remember from Section 2.2 that no space is necessary between the option (in this case -P) and the option argument (in this case spr).

```
$ lpr -Pspr order.eps
$
```

The following lpr command accomplishes the printing of the file named memol at the default printer.

```
$ lpr memol
$
```