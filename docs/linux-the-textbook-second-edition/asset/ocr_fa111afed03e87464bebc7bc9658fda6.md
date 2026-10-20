“(OH`

```
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

# **Exercise 6.3**

Insert the **student_records** file used in Section 6.2.1 in your current directory. Add to it ten more students’ records. Display the contents of this file by using the `cat student_records` and `cat -n student_records` commands. What is the difference between the outputs of the two commands?

# **Exercise 6.4**

Display the **student_records** file by using the `more` and `pr` commands. What command lines did you use?

# **Exercise 6.5**

Display the **/etc/passwd** file two lines before the line that contains your login name. What command line did you use?

# **Exercise 6.6**

Give commands for displaying the first and last seven lines of the **student_records** file.

# ### 6.3 Copying, Moving, and Removing Files

In this section, we describe commands for performing copy, as well as move/rename and remove/delete operations on files in a file structure. The commands discussed are `cp`, `mv`, and `rm`.