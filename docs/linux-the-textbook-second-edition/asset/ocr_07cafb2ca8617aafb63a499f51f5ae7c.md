+   -a, --all
+     do not ignore entries starting with .
+   
+   -A, --almost-all
+     do not list implied . and ..
+   
+   --author

# Manual page ls(1) line 1 (press h for help or q to quit)

This output from Linux is a Linux manual page, or man page, which gives a synopsis of the command usage showing the options, and a brief description that helps you understand how the command should be used. Typing q after one page has been displayed, as seen in the example, returns you to the command line prompt. Pressing the space key on the keyboard would have shown you more of the content of the manual pages, one screen at a time, related to the ls command.

To get help in using all the Linux commands and their options, use the man man command to go to the Linux reference manual pages.

The pages themselves are organized into eight sections, depending on the topic described and the topics that are applicable to the particular system. Table 2.1 lists the sections of the manual and what they contain. Most users find the pages they need in Section 1. Software developers mostly use library and system calls and thus find the pages they need in Sections 2 and 3. Users who work on document preparation get the most help from Section 7. Administrators mostly need to refer to pages in Sections 1, 4, 5, and 8.

The manual pages comprise multipage, specially formatted, descriptive documentation for every command, system call, and library call in Linux. This format consists of seven general parts: name, synopsis, description, list of files, related information, errors, warnings, and known bugs. You can use the man command to view the manual page for a command. Because of the name of this command, the manual pages are normally referred to as Linux man pages. When you display a manual page on the screen, the top-left corner of the page has the command name with the section it belongs to in parentheses, as with ls(1), seen at the top of the output manual page.

```
$ man passwd
```

The manual page for the passwd command now appears on the screen, but we do not show its output. Because they are multipage text documents, the manual pages for each topic take up more than one screen of text to display their entire contents. To see one screen of the manual page at a time, press the space bar on the keyboard. To quit viewing the manual page, press the Q key on the keyboard.

```
$ man pwd
```

| Section | What It Describes |
|---------|-------------------|
| 1       | User commands     |
| 2       | System calls      |
| 3       | Language library calls (C, FORTRAN, etc.) |
| 4       | Devices and network interfaces |
| 5       | File formats      |
| 6       | Games and demonstrations |
| 7       | Environments, tables, and macros for troff |
| 8       | System maintenance-related commands |