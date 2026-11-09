
```text
What server would you like to backup? loki
Backing up loki
Backup another server? (y/n) n
$
```

## Sum All the Numbers in a given Column of a Text

```sh
$ awk '{ sum += $1 } END { print sum }' file
$ cat file | awk '{ sum += $1 } END { print sum }'
```

Awk can be used to tally up a column of values. You can use this trick to add up all the disk space used across all the file systems on a given system, for example.

```text
$ df -mt ext4
Filesystem 1M-blocks Used Available Use% Mounted on
/dev/sda2  28215      3285      24644  12% /
/dev/sda1  485        55        406    12% /boot
$ df -mt ext4 | awk '{ sum += $3 } END { print sum }'
3340
$ sudo dmidecode --type memory
                Size: No Module Installed
                Size: 4096 MB
                Size: No Module Installed
                Size: 4096 MB
$ sudo dmidecode --type memory | grep 'Size:' | awk '{sum+=$2} END {print sum}'
8192
$
```

## Automatically Answer Yes to Any Command

```bash
$ yes | command
$ yes "string" | command
```

If you are trying to automate a process that requires user input, check out the yes command. By default yes simply prints out "y" until it is killed. You can make yes repeat any string. If you wanted to automatically answer "no" you could run "yes no."

```bash
$ ./install-my-app.sh
Are you sure you want to install my-app? (y/n) y
Ok, my-app installed.
$ yes | ./install-my-app.sh
Ok, my-app installed.
$
```

## Display Mounted File Systems in a Tabular Format

```bash
$ mount | column -t
```

The output of the mount command is not formatted in an easy-to-read manner. To make each column line up, pipe the output of the mount command to "column -t". By default mount displays all mounted filesystems, even the pseudo-filesystems like /proc and /sys. To limit output to a filesystem type, use the -t option and provide a type.

```bash
$ mount -t ext4
/dev/mapper/sys-lv_root on / type ext4 (rw)
/dev/sda1 on /boot type ext4 (rw)
$ mount -t ext4 | column -t
/dev/mapper/sys-lv_root on /      type ext4 (rw)
/dev/sda1                  on /boot type ext4 (rw)
```

## Kill All Processes for a given User or Program

```bash
$ pkill -9 command
$ pkill -u user command
```

If you need to kill several processes with the same command, use the `pkill` command. If you only want to kill processes for a given user, use the `-u` option. Pkill will only kill the processes when all the criteria match. That means you can kill all of a given process that is being run by a specific user.

```text
$ ps -ef | grep http | grep -v grep
root       12253       1  0 10:55 ?        00:00:00 /usr/sbin/httpd
apache     12255   12253  0 10:55 ?        00:00:00 /usr/sbin/httpd
apache     12256   12253  0 10:55 ?        00:00:00 /usr/sbin/httpd
apache     12257   12253  0 10:55 ?        00:00:00 /usr/sbin/httpd
apache     12258   12253  0 10:55 ?        00:00:00 /usr/sbin/httpd
apache     12259   12253  0 10:55 ?        00:00:00 /usr/sbin/httpd
apache     12260   12253  0 10:55 ?        00:00:00 /usr/sbin/httpd
apache     12261   12253  0 10:55 ?        00:00:00 /usr/sbin/httpd
apache     12262   12253  0 10:55 ?        00:00:00 /usr/sbin/httpd
$ sudo pkill -9 -f httpd
$ ps -ef | grep http | grep -v grep
$ ps -ef | grep ssh | grep -v grep

root          1202      1  0 Apr06 ?
00:00:00 /usr/sbin/sshd

root         12339  1202  0 11:22 ?
00:00:00 sshd: jason [priv]

jason        12342 12339  0 11:22 ?
00:00:00 sshd: jason@pts/0

root         12368  1202  1 11:23 ?
00:00:00 sshd: bob [priv]

bob          12372 12368  0 11:23 ?
00:00:00 sshd: bob@pts/1

$ sudo killall -u bob sshd
$ ps -ef | grep ssh | grep -v grep

root          1202      1  0 Apr06 ?
00:00:00 /usr/sbin/sshd

root         12339  1202  0 11:22 ?
00:00:00 sshd: jason [priv]

jason        12342 12339  0 11:22 ?
00:00:00 sshd: jason@pts/0
```

## Repeat a Command until it Succeeds

```bash
$ while true
> do
>   command && break
> done
```

The while loop will continue until the condition is false or it encounters a break. In this case we effectively create an infinite loop and break once our chosen command succeeds. If you want to keep pinging a host until it responds, you could use this while loop.

```bash
$ while true
> do
>     ping -c1 -W1 remote-host >/dev/null 2>&1 && break
> done ; echo "Remote-host is up at $(date)."
Remote-host is up at Fri Apr 11 21:30:29 EDT 2014.
$
```

If you're waiting for a file to show up on your server, you could use this while loop.

```bash
$ while true
> do
>     ls /srv/ftp/incoming/payroll.txt.gif 2>/dev/null && break
> done; echo "Payroll file arrived at $(date)."
Payroll file arrived at Fri Apr 11 21:33:23 EDT 2014.
```

## Find Who Is Using the Most Disk Space

```bash
$ sudo du -s /home/* | sort -n
```

This command will display the person who is using the most disk space in their home directory. The users with little disk space will be displayed at the top of your screen and the users using the most disk space will be displayed at the bottom.

```shell
$ sudo du -s /home/* | sort -n
32      /home/pat
32      /home/terry
40      /home/jim
40      /home/j?mob
44      /home/oracle
19184   /home/adminuser
22208   /home/bob
65132   /home/jason
$
```

If you are looking for a more graphical way to display disk usage, check out the neat utility ncdu.

```text
$ ncdu /home
ncdu 1.10 ~ Use the arrow keys to navigate, press ? for help
--- /home ---------------------------------------------
37.9GiB [##########] /ryan
 1.3MiB [          ] /lucas
Total disk usage: 37.9GiB  Apparent size: 37.8GiB
Items: 156055
```

## Find the Files That Are Using the Most Disk Space

```shell
$ find / -type f -exec wc -c {} \; | sort -n
```

Use find to execute the "wc -c" command against each file, revealing it's size in bytes, and then sort that output. The smallest files will be displayed first, and the largest files will be displayed last. If you are scanning every file on a system, this command could take awhile to complete.

```bash
$ sudo find /var -xdev -type f -exec wc -c {} \; | sort -n
0 /var/cache/apt/archives/lock
0 /var/cache/apt/pkgcache.bin
2572437 /var/lib/dpkg/available-old
6573098 /var/lib/dpkg/available
8433001 /var/cache/apt/pkgcache.bin
39872802 49659904 /var/cache/apt-xapian-index/index.1/termlist.db
62783488 /var/cache/apt-xapian-index/index.1/postlist.db
$ 
```

## List Processes, Sorted by Memory Usage

```bash
$ ps aux | sort -nk 4
```

Use this command to find the processes that are consuming the most memory. The processes using the least amount of memory will scroll off the top of your screen and the ones consuming the most amount of memory will be just above your shell prompt.

In this example, mysql is consuming 1.3% of the memory on this host.

```bash
$ ps aux | head -1
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
$ ps aux | sort -nk 4 | tail -5
root  2969  0.0  0.3  11856  3228 ?    Ss   17:16
0:00 sshd: jason [priv]
root  4576  0.0  0.3  11364  3380 ?    Ss   17:52
0:00 /usr/sbin/httpd
root   958  0.0  0.3  20844  4084 ?    Ssl  00:00
0:00 NetworkManager
root  1003  0.0  0.4  17104  4268 ?    Ssl  00:00
0:00 hald
mysql 4546  0.0  1.3 136332 13848 pts/0 Sl   17:52
0:01 /usr/libexec/mysqld
$
```

## List Processes, Sorted by CPU Usage

```shell
$ ps aux | sort -nk 3
```

Use this command to find the processes that are consuming the most CPU. The processes using the least amount of CPU will scroll off the top of your screen and the ones consuming the most amount of CPU will be just above your shell prompt.

In this example, mysqld is consuming 94% of the CPU on this host.

```text
$ ps aux | head -1
USER PID   %CPU %MEM       VSZ   RSS  TTY   STAT START TIME COMMAND
$ ps aux | sort -nk 3 | tail -5
root  2469  0.0  0.3  11856  3228 ?    Ss   17:16
0:00 /usr/sbin/fcoemon
root  4526  0.0  0.3  20844  4084 ?    Ssl  00:00
0:00 master
root  5571  2.1  0.3  11364  3380 ?    Ss   17:52
0:00 /usr/sbin/httpd
```
