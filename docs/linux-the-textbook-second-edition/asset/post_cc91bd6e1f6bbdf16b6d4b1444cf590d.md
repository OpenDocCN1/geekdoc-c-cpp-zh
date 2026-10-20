
## Basic File Processing

Like the head command, the tail command takes input from standard input if no file-list is given as an argument. The following session illustrates how the tail command can be used with and without options. We use the same sample file that we used for the head command. The tail sample command displays the last ten lines (the default tail size) of the sample file, and the tail -5 sample command displays the last five lines of the sample file. The tail +12 sample command displays the tail of the file starting with line number 12 (not the last 12 lines). Finally, the tail -5r sample command displays the last five lines of the sample file in reverse order.

```
$ tail sample
Queen
Rashid
Srini
Tang
Ursula
Vinny
Wang
X Window System
Yen
Zen
```

```
$ tail -5 sample
Vinny
Wang
X Window System
Yen
Zen
```

```
$ tail +12 sample
Lisa
Mike
Nadeem
Oram
Paul
Queen
Rashid
Srini
Tang
Ursula
Vinny
Wang
X Window System
Yen
Zen
```

```
$ tail -5r sample
Zen
Yen
X Window System
Wang
Vinny
```

The following commands show that files otto and data have proper PostScript and uuencoded tails.

```
$ tail -5 otto
8 f3
( ) show
pagelevel restore
showpage
%EOF
```

```
$ tail data
M;W4@:&%V90IN;W0@=')I960@;W5T(&90<B!L;VYG('!I;64N('!;W=E=F5R
M4"!T;R!B92!S=6-C97-S9G5L.+"!;W4@;75S="!T<@I(96QL;RP@5V]R;&@A
`(OH`
end
$
```

The **-f** option of the `tail` command is very useful if you need to see the tail of a file that is growing. This situation occurs quite often when you run a simulation program that takes a long time to finish (several minutes, hours, or days) and you want to see the data produced by the program as it is generated. It is convenient to do so if your Linux system runs the X Window System (see Chapter W28). In an X environment, you can run the `tail` command in an *xterm* (a console window) to monitor the newly generated data as it is generated and keep doing your other work concurrently. The following command displays the last ten lines of the **sim.data** file and displays new lines as they are appended to the file. You can terminate the command by pressing `<Ctrl+C>`.

```
$ tail -f sim.data
... last 10 lines of sim.data ...
... more data as it is appended to sim.data ...
```

Sometimes, while identifying problems in a Linux system, the system administrator needs to display files in the **/var** directory that keep growing because the kernel and applications keep appending new messages to them, including files in the **/var/spool**, **/var/mail**, and **/var/log** directories.

Traditionally, the system administrators are able to view these files as they are appended using the `tail -f` command, as in the following session to display the last ten lines in the **/var/log/messages** file and continue to show new messages from the kernel and applications as they are appended to this file.

```
$ tail -f /var/log/messages
... last 10 lines of /var/log/messages ...
... more data as it is appended to /var/log/messages ...
```

Using systemd, available in all major branches of Linux, the system administrators can also use the `journalctl -f` command to display messages being written to the system log in real time. It is possible, using the `journalctl -r` command, to view the last or most recent lines written to the system log. We show more uses of journalctl in Chapter 18, and Chapter W27 at the book website, on systemd.

In the following in-chapter exercises, you are asked to use the cat, head, more, pr, and tail commands for displaying different parts of text files, with and without page titles and numbers.

### Exercise 6.3

Insert the **student_records** file used in Section 6.2.1 in your current directory. Add to it ten more students’ records. Display the contents of this file by using the `cat student_records` and `cat -n student_records` commands. What is the difference between the outputs of the two commands?

### Exercise 6.4

Display the **student_records** file by using the `more` and `pr` commands. What command lines did you use?

### Exercise 6.5

Display the **/etc/passwd** file two lines before the line that contains your login name. What command line did you use?

### Exercise 6.6

Give commands for displaying the first and last seven lines of the **student_records** file.

### 6.3 Copying, Moving, and Removing Files

In this section, we describe commands for performing copy, as well as move/rename and remove/delete operations on files in a file structure. The commands discussed are `cp`, `mv`, and `rm`.

#### 6.3.1 Copying Files

The Linux command for copying files is cp. The following is a brief description of the command.

**Syntax:** `cp [options] file1 file2`

**Purpose:** Copy file1 to file2. If file2 is a directory, make a copy of file1 in this directory.

**Commonly used options/features:**
- `-f` Force copying if there is no write permission on file2
- `-i` If file2 exists, prompt before overwriting
- `-p` Preserve file attributes such as owner ID, group ID, permissions, and modification times
- `-r` Recursively copy files and subdirectories

You must have permission to read the source file (file1) and permission to execute (search) the directories that contain file1 and file2. In addition, you must have the write permission for the directory that contains file2 if it does not already exist. If file2 exists, you don’t need the write permission to the directory that contains it, but you must have the write permission to file2. If the destination file (file2) exists, by default, it will be overwritten without informing you if you have permission to write to the file. To be prompted before an existing file is overwritten, you need to use the -i option. If you do not have permission to write to the destination file, you will be informed of this. If you do not have permission to read the source file, an error message will appear on your screen.

The following cp command line makes a copy of temp in temp.bak. The ls commands show the state of the current directory before and after execution of the cp command. Figure 6.1 shows the same information in pictorial form.

```
$ ls
memo  sample  temp
$ cp temp temp.bak
$ ls
memo  sample  temp  temp.bak
$
```

The command returns an error message if temp does not exist or if it exists but you do not have permission to read its content. The command also returns an error message if temp.bak exists and you do not have permission to write to it. The following session illustrates these points. The first error message is reported because the letter file does not exist in the current directory. The second error message is reported because you do not have permission to read the sample file. The last command reports an error message because temp.bak exists and you do not have write permission for it. You can override the absence of write permission and force copying by using the -f option, as shown in the next command. The ls -l memo temp.bak command is used to show that the copying has actually taken place; that is,

![](img/2a18e06cd9c6395e451f26126ecba1fd_157_0.png)

FIGURE 6.1 State of the current directory before and after the temp file has been copied to temp.bak.

the data has been copied, but the time stamp for the file is the current time. If you want to copy both the data and attributes of the source file, you need to use the cp command with -f and -p options, as in the last cp command that follows. The last ls -l memo temp.bak command is used to show that both data and file attributes, such as the time stamp, have been copied.

```
$ ls -l
total 3
-rwxr----- 1 sarwar faculty 371 Aug 28 07:01 memo
--wxr----- 1 sarwar faculty 164 Jul 25 12:35 sample
-r-xr----- 1 sarwar faculty 792 Aug 28 07:01 temp
-r-xr----- 1 sarwar faculty 792 Aug 28 07:05 temp.bak
$ cp letter letter.bak
cp: letter: No such file or directory
$ cp sample sample.new
cp: sample: Permission denied
$ cp memo temp.bak
cp: temp.bak: Permission denied
$ cp -f memo temp.bak
$ ls -l memo temp.bak
-rwxr----- 1 sarwar faculty 371 Aug 28 07:01 memo
-rwxr----- 1 sarwar faculty 371 Aug 28 07:22 temp.bak
$ cp -fp memo temp.bak
$ ls -l memo temp.bak
-rwxr----- 1 sarwar faculty 371 Aug 28 07:01 memo
-rwxr----- 1 sarwar faculty 371 Aug 28 07:01 temp.bak
$
```

The following command makes a copy of the .profile file in your home directory and puts it in the .profile.bak file in the sys.backups subdirectory, also in your home directory. This command works regardless of the directory you are in when you run the command because the pathname starts with your home directory. You should execute this command before changing your runtime environment specified in the ~/.profile file, so that you have a backup copy of the previous working environment in case something goes wrong when you set up the new environment. The command produces an error message if ~/.profile does not exist, if you do not have permission to read it, if the ~/sys.backups directory does not exist or you do not have the execute (search) and write permissions for it, or if .profile.bak exists but you do not have write permission to it.

```
$ cp ~/.profile ~/sys.backups/.profile.bak
$
```

The following command copies all the files in the current directory, starting with the string lab to the directory ~/courses/ee446/backups. The command also prompts you for overwriting if any of the source files already exist in the backups directory. In this case (in which multiple files are being copied), if backups is not a directory, or if it does not exist, an error message is displayed on the screen informing you that the target must be a directory.

```
$ cp -i lab* ~/courses/ee446/backups
$
```

If you want to copy a complete directory to another directory, you need to use the cp command with the -r option. This option recursively copies files and subdirectories from the source directory to the destination directory. It is a useful option that you can use to create backups of important directories periodically. Thus, the following command recursively copies the ~/courses directory to the ~/backups directory.

```
$ cp -r ~/courses ~/backups
$
```
