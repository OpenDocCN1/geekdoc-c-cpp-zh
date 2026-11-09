
```text
mysql 4447 94 12.8 2134672 1031064 ?  Sl  10:52
27:39 /usr/libexec/mysqld
$
```

### Quickly Tell If You Are on a 32 Bit or 64 Bit System

```bash
$ getconf LONG_BIT
```

If you're on a system and need to know if it's 32 or 64 bit, use getconf.

```bash
$ getconf LONG_BIT
32
$ ssh remote-host getconf LONG_BIT
64
```

### Generate a Random Password

```bash
$ openssl rand -base64 48 | cut -c1-PASSWORD_LENGTH
$ gpw () { openssl rand -base64 48 | cut -c1-${1}; }
```

You can use the openssl command to generate a random password. If you find yourself doing this often, you can create a function. Simply pass in how long you want the password to be.

```bash
$ echo 'gpw () {openssl rand -base64 48 | cut -c1-${1};
}' >> ~/.bash_profile
$ . ~/.bash_profile
$ gpw
t3EjyxKXH3bz3VdR7G8NV3fMvZpXLOvT+AqWgQnw9pLm/UaRNhicPB
jKQsr26.3k
$ gpw 6
ua2Z0
```

## FILES AND DIRECTORIES

### Quickly Make a Backup of a File

```bash
$ cp file{,.bak}
```

You can use brace expansion to quickly create a backup copy of a file. Brace expansion allows you to create multiple command line arguments from a single argument. The single argument is combined with all the strings that are given within the braces and creates as many new arguments as brace strings. Values in the braces can either be comma separated strings or a sequence expression. Examples of sequence expressions include {1..5} and {a..z}.

```bash
$ sudo cp /etc/passwd{,.bak}
$ ls /etc/passwd*
/etc/passwd  /etc/passwd.bak
$ mkdir -p ~/my-app/{bin,lib,log}
$ ls ~/my-app/
bin  lib  log
$ echo 10.0.0.{0..7}
10.0.0.0 10.0.0.1 10.0.0.2 10.0.0.3 10.0.0.4 10.0.0.5
10.0.0.6 10.0.0.7
```

### Quickly Change a File's Extension

```bash
$ mv file.old{,.new}
```

To rename a file with a new extension employ brace expansion. This example changes a ".txt" file to a ".doc" file.

```bash
$ ls report*
report.txt
$ mv report.{txt,doc}
$ ls report*
report.doc
$
```

Here's another example.

```bash
$ ls httpd*
httpd.cfg
$ mv httpd.{cfg,conf}
$ ls httpd*
httpd.conf
$
```

This command will add an extension to a file.

```bash
$ ls jazz*
jazz
$ mv jazz{,.mp3}
$ ls jazz*
jazz.mp3
$
```

### Create Backups of Files by Date with Ease

```bash
$ alias d='date +%F'
```

By using the date format of YYYY-MM-DD for file or directory names, you make ls output more human friendly. You can quickly tell the date order of the files when using this format.

```bash
$ ls -l file*
file.2013-04-08
file.2013-12-21
file.2014-04-08
$ ls -l other-file.*
other-file.04-08-2013
other-file.04-08-2014
other-file.12-23-2013
```

Before making a change to a file I like to make a backup copy of it. I also like to know when I made the backup. By creating an alias of "d" which is short for the date in YYYY-MM-DD format, I can quickly create these types of backups.

```bash
$ echo "alias d='date +%F'" >> ~/.bash_profile
$ . ~/.bash_profile
$ d
2014-04-08
$ sudo cp httpd.conf httpd.conf.`date`
$ sudo cp httpd.conf httpd.conf.$(date)
$ sudo cp httpd.conf !#.$(date)
$ sudo cp httpd.conf !-.$(date)
$ ls -l httpd.conf*
httpd.conf
httpd.conf.2014-04-08
```

### Overwrite the Contents of a File

```bash
$ command > file
```

You can redirect output from one command to a file using the greater-than symbol. A single greater-than symbol (>) redirects standard output to a file, overwriting (truncating) any existing contents of the file. If no file exists, it creates one.

```bash
$ grep bash /etc/passwd > users-that-use-bash
$ cat users-that-use-bash
root:x:0:0:root:/root:/bin/bash
jason:x:501:501:Jason:/home/jason:/bin/bash
oracle:x:1006:1006::/home/oracle:/bin/bash
bob:x:1000:1000:Bob Smith:/home/bob:/bin/bash
$
```

### Empty a File That Is Being Written To

```bash
$ > file
$ cat /dev/null > file
```

To quickly zero out a file you can redirect nothing to it. Why not just delete the file and recreate it? If a process has a file open when you delete it, the process will keep the file handle open and continue writing to that file. Only when the process closes the file handle will the disk space used by that file be freed. If an application fills up /var and you delete the open log file, /var will still be full. If you redirect nothing to the file, the file is truncated and the application can continue writing to the file.

```bash
$ sudo -s
# > /var/log/maillog
# ls -l maillog

-rw-------. 1 root root 0 Apr 9 18:55 maillog
```

### Append a String to a File

```bash
$ command >> file
```

The double greater than sign (>>) redirects standard output to a file and appends to any existing contents. If no file exists, it creates one.

```bash
$ echo build new server >> todo.txt
$ cat todo.txt
build new server
$ echo add server to the load balancer >> todo.txt
$ cat todo.txt
build new server
add server to the load balancer
$
```

### Follow a File as It Grows

```bash
$ tail -f file
```

For a file that is constantly being updated like a log file, use tail -f to view the updates to the file in real time.

```bash
$ tail -f /var/log/syslog
Apr 10 21:45:01 linwwwl CRON[31769]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
Apr 10 21:46:28 linwwwl whoopsie[1421]: online
Apr 10 21:47:37 whoopsie[1421]: last message repeated 2 times
Apr 10 21:55:01 linwwwl CRON[32548]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
Apr 10 22:05:01 linwwwl CRON[931]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
Apr 10 22:15:01 linwwwl CRON[2459]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
Apr 10 22:17:01 linwwwl CRON[2609]: (root) CMD (   cd / && run-parts --report /etc/cron.hourly)
Apr 10 22:25:01 linwwwl CRON[3197]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
Apr 10 22:35:01 linwwwl CRON[4036]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
Apr 10 22:35:33 linwwwl whoopsie[1421]: online
```

### Watch Multiple Log Files at the Same Time

```bash
$ multitail file1 fileN
$ multitail file1 -I fileN
```

The multitail command allows you to browse through several files at once. Not only does multitail allow you to watch multiple files, it supports color highlighting, filtering, merging, and more. Here is a quick rundown of some of the most helpful commands for multitail.

- F1 - Help
- a - Add another file to follow
- d - Delete a file from the view
- / - Start a search (Find)
- ctrl-g - Edit a command, menu, or action. Similar to the emacs ctrl-g key binding.
- q - Quit

```bash
$ sudo multitail /var/log/syslog  /var/log/kern.log

Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info>
(eth0): IPv6 addrconf timed out or failed.

Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info>
Activation (eth0) Stage 4 of 5 (IPv6 Configure
Timeout) scheduled...

Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info>
Activation (eth0) Stage 4 of 5 (IPv6 Configure
Timeout) started...

Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info>
Activation (eth0) Stage 4 of 5 (IPv6 Configure
Timeout) complete.
001 /var/log/syslog *Press F1/<CTRL>+<h> for help*
132KB - 2014/04/19 12:46:45

Apr 19 12:43:08 linuxsvr kernel: [    10.012891]
Console: switching to colour frame buffer device
240x67

Apr 19 12:43:08 linuxsvr kernel: [    10.012926] fb0:
VESA VGA frame buffer device

Apr 19 12:43:11 linuxsvr kernel: [    12.288420] hda-
intel: Invalid position buffer, using LPIB read
method instead.
Apr 19 12:43:17 linuxsvr kernel: [ 18.891011] hda-
intel: IRQ timing workaround is activated for card
#0. Suggest a bigger bdl_pos_adj.
01] /var/log/kern.log *Press F1/<CTRL><h> for help*
132KB - 2014/04/19 12:46:45
```

To merge multiple files into one window, use the "-I" option. This intermixes the output of both of the files. This can aid in troubleshooting a problem.

```bash
$ sudo multitail /var/log/syslog -I /var/log/kern.log
Apr 19 12:43:08 linuxsvr kernel: [ 10.012891]
Console: switching to colour frame buffer device
240x67
Apr 19 12:43:08 linuxsvr kernel: [ 10.012926] fb0:
VESA VGA frame buffer device
Apr 19 12:43:11 linuxsvr kernel: [ 12.288420] hda-
intel: Invalid position buffer, using LPIB read
method instead.
Apr 19 12:43:17 linuxsvr kernel: [ 18.891011] hda-
intel: IRQ timing workaround is activated for card
#0. Suggest a bigger bdl_pos_adj.
Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info>
Activation (eth0) Stage 4 of 5 (IPv6 Configure
Timeout) complete.
Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info>
Activation (eth0) Stage 4 of 5 (IPv6 Configure
Timeout) scheduled...
Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info>
Activation (eth0) Stage 4 of 5 (IPv6 Configure
Timeout) started...
Apr 19 12:43:29 linuxsvr NetworkManager[758]: <info>
(eth0): IPv6 address timed out or failed.
```
