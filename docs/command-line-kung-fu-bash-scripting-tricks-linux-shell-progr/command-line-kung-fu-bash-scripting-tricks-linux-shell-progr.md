# 命令行功夫：Bash 脚本技巧、Linux Shell 编程提示与 Bash 单行命令

## 您的免费礼物

作为感谢你阅读*命令行功夫*，我想赠送你一本*Windows 应用程序的 Linux 替代方案*。在书中，你将了解到当今 Linux 上 50 多款最受欢迎的应用程序。这些应用程序可让你浏览网页、看电影、听音乐、连接你喜爱的社交网络、制作演示文稿等。这份礼物是本书的完美补充，将助你踏上 Linux 之旅。请访问 [http://www.linuxtrainingacademy.com/linux-apps](http://www.linuxtrainingacademy.com/linux-apps) 下载你的免费礼物。

## 简介

自 20 世纪 90 年代以来，我一直在 Unix 和 Linux 系统的命令行上工作。不用说，只要有一个美元符号和一个闪烁的光标盯着我，我就感到非常自在。多年来，我掌握了一些命令行“技巧”，它们为我节省了时间，也减少了挫败感。

其中一些技巧源于必要——我实在有太多工作要完成，而完成它们的时间又太少。另一些则模仿了计算机编程和应用程序开发中常见的模式。其余的是我的命令行偶像和导师直接或间接分享给我的。通过观察、模仿并听取一位经验丰富的 Unix 和 Linux 专业人士的建议，你能学到的东西令人惊叹。

尽管书名为*命令行功夫*，你并不需要成为 Linux 忍者才能使用本书介绍的策略。这些技巧按书中呈现的方式即可奏效。你无需完全理解所有细节和细微之处，就可以立即开始使用它们。不过，如果你想要或需要更多信息，每个技巧后面都附有解释和实际应用示例。

此外，如果你想看其中一些命令的实际运行，请访问 [http://www.linuxtrainingacademy.com/fu](http://www.linuxtrainingacademy.com/fu)。在那里你会找到一系列视频，演示本书涵盖的一些命令。

最后，如果你想概览 Linux 命令行和操作系统，请阅读我的另一本书*Linux 入门*。它将为你打下坚实的基础，让你在此基础上提升 Linux 技能。

让我们开始吧。

## Shell 历史

### 以 root 身份运行最后一条命令

```sh
$ sudo !!
$ su -c "!!"
```

如果你忘了用 root 权限运行某条命令，只需使用 sudo !! 或 su -c "!!" 重复执行它即可。

```sh
$ adduser sam
-bash: /usr/sbin/adduser: Permission denied
$ sudo !!
sudo adduser sam
$ id sam
uid=1007(sam) gid=1007(sam) groups=1007(sam)
$ userdel -r sam
-bash: /usr/sbin/userdel: Permission denied
$ sudo !!
sudo userdel -r sam
$ id sam
id: sam: No such user
$ useradd jim
-bash: /usr/sbin/useradd: Permission denied
$ su -c "useradd jim"
Password:
$ id jim
uid=1007(jim) gid=1007(jim) groups=1007(jim)
```

这种感叹号语法称为事件指示符。事件指示符引用 shell 历史中的某条命令。Bang-Bang（!!）会重复最近一条命令，但我最喜欢的事件指示符用法之一，是运行最近一条以给定字符串开头的命令。下面是一个示例。

```bash
$ whoami
jason
$ uptime
12:33:15 up 35 min, 1 user, load average: 0.00, 0.00, 0.00
$ df -hT /boot
Filesystem Type Size Used Avail Use% Mounted on
/dev/vda1 ext4 485M 55M 406M 12% /boot
$ !u
uptime
12:33:29 up 35 min, 1 user, load average: 0.00, 0.00, 0.00
```

```bash
$ sudo !w
sudo whoami
root
```

### 重复上一条以给定字符串开头的命令

```bash
$ !<string>
```

这是事件指示符的另一个示例。要调出最近一条以 `<string>` 开头的命令，请运行“!<string>”。你可以只指定首字母，也可以指定足以使其唯一的字符串部分。这个示例演示了这一概念。

```text
$ who
jason       pts/1   2014-04-06 21:04 (192.168.1.117)
$ w
jason       pts/1       192.168.1.117 21:04 0.00s
0.33s 0.00s w
$ !w
w
jason       pts/1       192.168.1.117 21:04 0.00s
0.33s 0.00s w
$ !wh
who
jason       pts/1   2014-04-06 21:04 (192.168.1.117)
```

下面是一个实际示例：你检查某个进程是否正在运行，将其终止，然后确认它确实已停止。

```text
$ ps -fu apache
UID   PID  PPID  C STIME TTY  TIME     CMD
apache 1877 1879 0 21:32 ?    00:00:00
/usr/sbin/httpd
apache 2879 1    0 21:32 ?    00:00:00
/usr/sbin/httpd
$ sudo service httpd stop
Stopping httpd:        [  OK  ]
$ !p
ps -fu apache

UID   PID  PPID  C STIME TTY  TIME     CMD
$
```

### 复用上一条命令中的第二个单词（第一个参数）

```text
$ !^
```

如果你需要取用上一条命令中的第二个单词，可以使用“!^”单词指示符。无论你在哪里使用“!^”，它都会被替换为上一条命令中的第二个单词。你也可以把它理解为上一条命令的第一个参数。

```text
$ host www.google.com 8.8.8.8
Using domain server:
Name: 8.8.8.8
Address: 8.8.8.8#53
Aliases:
www.google.com has address 173.194.46.83
www.google.com has address 173.194.46.81
www.google.com has address 173.194.46.84
www.google.com has address 173.194.46.82
www.google.com has address 173.194.46.80
www.google.com has IPv6 address
2607:f8b0:4009:805::1013
$ ping -c1 !^
ping -c1 www.google.com
PING www.google.com (173.194.46.80) 56(84) bytes of data.

64 bytes from ord08s11-in-f16.1e100.net
(173.194.46.80): icmp_seq=1 ttl=51 time=17.0 ms

--- www.google.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss,
time 49ms

rtt min/avg/max/mdev = 17.071/17.071/17.071/0.000 ms
$
```

### 复用上一条命令中的最后一个单词（最后一个参数）

```text
$ !$
```

我常常发现自己需要对上一条命令行中的最后一项执行另一项操作。要在当前命令中访问该项，请使用“!$”。

```text
$ unzip tpsreport.zip
Archive: tpsreport.zip
  inflating: cover-sheet.doc
$ rm !$
rm tpsreport.zip
$ mv cover-sheet.doc reports/
$ du -sh !$
du -sh reports/
4.7G  reports/
$
```

### 复用之前某条命令中的第 N 个单词

```bash
$ !!:N
$ <event_designator>:<number>
```

要访问上一条命令中的某个单词，请使用“!!:N”，其中 N 是你想取用的单词编号。第一个单词是 0，第二个单词是 1，依此类推。你可以把 0 看作命令本身，把 1 看作命令的第一个参数，把 2 看作第二个参数，以此类推。

你可以将任何事件指示符与单词指示符结合使用。在下面的示例中，“!!”是最近一条命令行：avconv -i screencast.mp4 podcast.mp3。“!a”事件指示符会展开为同一条命令，因为它是最近一条以字母“a”开头的命令。

```bash
$ avconv -i screencast.mp4 podcast.mp3
$ mv !!:2 converted/
mv screencast.mp4 converted/
$ mv !a:3 podcasts/
mv podcast.mp3 podcasts/
$
```

### 在替换字符串的同时重复上一条命令

```bash
$ ^<string1>^<string2>^
```

这个小技巧非常适合快速纠正输入错误。如果省略 ^<string2>，那么 <string1> 将从上一命令中删除。通过

默认情况下，仅替换 <string1> 的第一次出现。要替换所有出现，请追加“^&”。可以省略末尾的脱字符符号，但使用“^&”时除外。

```bash
$ grpe jason /etc/passwd
-bash: grpe: command not found
$ ^pe^ep
grep jason /etc/passwd
jason:x:501:501:Jason Cannon:/home/jason:/bin/bash
$ grep rooty /etc/passwd
$ ^y
grep root /etc/passwd
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root:/sbin/nologin
$ grep cannon /etc/passwd ; ls -ld /home/cannon
ls: cannot access /home/cannon: No such file or directory
$ ^cannon^cannon^&
grep cannon /etc/passwd ; ls -ld /home/cannon
cannon:x:1001:1001::/home/cannon:/bin/sh
drwxr-xr-x 2 cannon ball 4096 Apr  7 00:22 /home/cannon
```

### 引用当前命令中的某个词并复用它

```bash
$ !#:N
```

“#”事件指示符表示当前命令行，而 :N 词指示符表示命令行上的某个词。词引用从零开始，因此第一个词（几乎总是命令）是 :0，第二个词（或命令的第一个参数）是 :1，依此类推。

### 保存命令行会话副本

```sh
$ mv Working-with-Files.pdf Chapter-18-Working-with-Files.pdf
```

如果要记录屏幕上看到的内容，请使用 script 命令。script 命令会捕获终端上打印的所有内容并将其保存到文件中。可以将文件名作为参数提供给 script，或让它创建名为 typescript 的默认文件。

```text
$ script
Script started, file is typescript
$ cd /usr/local/bin
$ sudo ./upgradedb.sh
sudo password for jason:
Starting database upgrade.
...
Database upgrade complete.
$ exit
exit
Script done, file is typescript
$ cat typescript
Script started on Wed 09 Apr 2014 06:30:58 PM EDT
$ cd /usr/local/bin
$ sudo ./upgradedb.sh
sudo password for jason:
Starting database upgrade.
...
Database upgrade complete.
$ exit
exit
Script done on Wed 09 Apr 2014 06:31:44 PM EDT
$
```

### 找出最常用的命令

要获取 Shell 历史记录中使用最多的前十命令列表，请使用以下命令。

```bash
$ history | awk '{print $2}' | sort | uniq -c | sort -rn | head
```

```bash
$ history | awk '{print $2}' | sort | uniq -c | sort -rn | head
     61 ls
     45 cd
     40 cat
     31 vi
     24 ip
     22 sudo
     22 ssh
     22 ll
     19 rm
     17 find
$
```

### 清空 Shell 历史记录

```bash
$ history -c
```

要清空 Shell 历史记录，请使用 history 命令的 -c 选项。

```bash
$ history | tail -5
  966  ls -lR Music/
  967  find Music/ -type f -ls
  968  dstat
  969  sudo vi /etc/motd
  970  cd ..
  971  sudo du -s /home/* | sort -n
$ history -c
$ history
     1  history
$
```

## 文本处理与操作

### 去除注释和空行

```bash
$ grep -E -v "^#|^$" file
```

要去除配置文件中的所有干扰内容，请去掉注释和空行。这两个正则表达式（regex）可以做到这一点。“^#”匹配所有以“#”开头的行。“^$”匹配所有空行。grep 的 -E 选项允许我们使用正则表达式，-v 选项则反转匹配结果。

```bash
[jason@www conf]$ grep -E -v "^#|^$" httpd.conf | head

ServerTokens OS
ServerRoot "/etc/httpd"
PidFile run/httpd.pid
Timeout 60
KeepAlive Off
MaxKeepAliveRequests 100
KeepAliveTimeout 15
<IfModule prefork.c>
StartServers          8
MinSpareServers       5
[jason@www conf]$
```

### 使用 Vim 通过网络编辑文件

```bash
$ vim scp://remote-host//path/to/file
$ vim scp://remote-user@remote-host//path/to/file
```

如果要通过 SSH 使用 vim 编辑文件，可以让它承担来回复制文件的重任。

```bash
$ vim scp://linuxserver//home/jason/notes.txt
```

### 以表格形式显示输出

```bash
$ alias ct='column -t'
$ command | ct
```

使用 column 命令将文本格式化为多列。通过使用 -t 选项，column 会统计输入包含的列数，并创建具有该列数的表格。这确实可以让许多命令的输出更易读。我发现自己经常使用它，因此为该命令创建了一个别名。

```bash
$ alias ct='column -t'
$ echo -e 'one two\nthree four'
one two
three four
$ echo -e 'one two\nthree four' | ct
one    two
three four
$ mount -t ext4
/dev/vda2 on / type ext4 (rw)
/dev/vda1 on /boot type ext4 (rw)
$ mount -t ext4 | cat
/dev/vda2 on / type ext4 (rw)
/dev/vda1 on /boot type ext4 (rw)
$
```

### 获取输出行中的最后一个词

```bash
$ awk '{print $NF}' file
$ cat file | awk '{print $NF}'
```

可以使用 $FIELD_NUMBER 表示法让 awk 打印字段。要打印第一个字段，使用 $1；打印第二个字段，使用 $2，依此类推。但是，如果你不知道字段数，或者不想数它们，请使用 $NF，它表示字段总数。Awk 以空格分隔字段，但你可以使用 -F 参数改变该行为。以下是如何打印系统上正在使用的所有 shell。使用冒号作为字段分隔符，然后打印最后一个字段。

```bash
$ awk -F: '{print $NF}' /etc/passwd | sort -u
```

如果要显示系统上每个用户的 shell，可以这样做。

```bash
$ awk -F: '{print $1,$NF}' /etc/passwd | sort | column -t
adm                    /sbin/nologin
apache              /sbin/nologin
avahi-autoipd       /sbin/nologin
bin                 /sbin/nologin
bobb                /bin/bash
...
```

### 使用 Less 查看彩色输出

```bash
$ ls --color=always | less -R
$ grep --color=always file | less -R
```

某些 Linux 发行版会为 ls 和 grep 创建带有 --color=auto 选项的别名。这会导致仅在输出到终端时才使用颜色。当你通过管道传输 ls 或 grep 的输出时，不会发出颜色代码。可以通过 ls 或 grep 的 --color=always 强制始终显示颜色。要让 less 命令显示创建颜色的原始控制字符，请使用 -R 选项。

```bash
$ grep --color=always -i bob /etc/passwd | less -R
$ ls --color=always -i /etc | less -R
```

### 管道传输到 Grep 时保留颜色

```bash
$ ls -l --color=always | grep --color=never string
```

如果将彩色输入通过管道传输到 grep，并且 grep 是带有 --color=auto 选项的别名，grep 会丢弃输入中的颜色，并高亮显示所搜索的字符串。为了保留彩色输入，请使用 --color=never 选项强制 grep 不使用颜色。

```bash
$ ls -l --color=always *.mp3 | grep --color=never jazz
-rw-r--r-- 1 jason jason 21267371 Feb 16 11:12 jazz-album-1.mp3
```

### 使用 Sudo 向文件追加文本

```bash
echo text | sudo tee -a file
```

如果你曾经尝试在“sudo echo”命令之后使用重定向向文件追加文本，你很快会发现那行不通。发生的情况是，echo 语句以 root 身份执行，但重定向以你自己的身份发生。

```bash
sudo echo "PRODUCTION Environment" >> /etc/motd
-bash: /etc/motd: Permission denied
```

幸运的是，可以将 sudo 与 tee 命令结合使用来向文件追加文本。

```bash
echo "PRODUCTION Environment" | sudo tee -a /etc/motd
PRODUCTION Environment
```

### 更改字符串大小写

```bash
tr [:upper:] [:lower:]
tr [:lower:] [:upper:]
```

当需要更改字符串的大小写时，请使用 tr 命令。可以向 tr 提供范围，如“tr a-z A-Z”，或使用“tr [:lower:] [:upper:]”。

```bash
ENVIRONMENT=PRODUCTION
$ DIRECTORY=$(echo $ENVIRONMENT | tr [:upper:] [:lower:])
$ echo $ENVIRONMENT | sudo tee -a /etc/motd
$ tail -1 /etc/motd
PRODUCTION
$ sudo mkdir /var/www/$DIRECTORY
$ sudo tar zxf wwwfiles.tgz -C /var/www/$DIRECTORY
```

### 以人类可读格式显示命令搜索路径

```bash
$ echo $PATH | tr ':' '\n'
```

阅读冒号分隔的项列表对人类来说不如对计算机那么容易。要用换行符替换冒号，请使用 tr 命令。

```bash
$ echo $PATH
/usr/bin:/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin
$ echo $PATH | tr ':' '\n'
/usr/bin
/bin
/usr/local/bin
/bin
/usr/bin
/usr/local/sbin
/usr/sbin
/sbin
```




### 使用编辑器

```bash
$ cat > file
<ctrl-d>
```

如果你需要快速记一笔，而不需要功能完备的文本编辑器，可以直接使用 cat 并将输出重定向到文件。完成后按 <ctrl-d> 即可创建该文件。

```bash
$ cat > shopping.list
eggs
bacon
coffee
<ctrl-d>
$ cat shopping.list
eggs
bacon
coffee
$
```

### 显示两个字符串之间的一段文本

```bash
$ awk '/start-pattern/,/stop-pattern/' file.txt
$ command | awk '/start-pattern/,/stop-pattern/'
```

grep 命令非常适合提取单行文本。但如果你需要捕获整块文本呢？使用 awk 并为其提供起始和停止模式。模式可以只是一个字符串，甚至可以是正则表达式。

```bash
$ sudo dmidecode | awk '/Processor/,/Manual/'
Processor Information
        Socket Designation: SOCKET 0
        Type: Central Processor
        Family: Core i5
        Manufacturer: Intel
$ awk '/worker.c/,/^$/' httpd.conf
<IfModule worker.c>
StartServers             4
MaxClients             300
MinSpareThreads         25
MaxSpareThreads         75
ThreadsPerChild         25
MaxRequestsPerChild      0
</IfModule>
$
```

### 删除两个字符串之间的一段文本

```shell
$ sed '/start-pattern/,/stop-pattern/d' file

$ command | sed '/start-pattern/,/stop-pattern/d'
file
```

通过为 sed 命令提供起始和停止模式，并让它删除整个范围，你可以删除一段文本。模式可以是字符串或正则表达式。此示例删除前七行，因为 "#" 匹配第一行，而 "^$" 匹配第七行。

```shell
$ cat ports.conf

# If you just change the port or add more ports here,
you will likely also
# have to change the VirtualHost statement in
# /etc/apache2/sites-enabled/000-default

# This is also true if you have upgraded from before
# 2.2.9-3 (etch). See /usr/share/doc/apache2.2-
# common/NEWS.Debian.gz and
# README.Debian.gz
NameVirtualHost *:80
Listen 80
<IfModule mod_ssl.c>
        # If you add NameVirtualHost *:443 here, you
will also have to change
        # the VirtualHost statement in
/etc/apache2/sites-available/default-ssl
        # to <VirtualHost *:443>
        # Server Name Indication for SSL named
virtual hosts is currently not
        # supported by MSIE on Windows XP.
        Listen 443
</IfModule>
<IfModule mod_gnutls.c>
        Listen 443
</IfModule>
$ sed '/^#\|^$/d' ports.conf
NameVirtualHost *:80
Listen 80
<IfModule mod_ssl.c>
<IfModule mod_gnutls.c>
        Listen 443
</IfModule>
</IfModule>
```

### 使用别名修复常见拼写错误

```bash
$ alias typo='correct spelling'
```

如果你发现自己一遍又一遍地犯同样的输入错误，可以用别名来修正它。

```bash
$ grep root /etc/passwd
bash: grep: command not found
$ echo "alias grep='grep'" >> ~/.bash_profile
$ ~/.bash_profile
$ grep root /etc/passwd
root:x:0:0:root:/root:/bin/bash
$
```

### 在保持首行表头完整的同时对输出正文排序

将此函数添加到你的个人初始化文件中，例如 `~/.bash_profile`：

```bash
body() {
    IFS= read -r header
    printf '%s\n' "$header"
    "$@"
}
$ command | body sort
$ cat file | body sort
```

我常常希望对包含表头的命令输出进行排序。执行排序后，表头会和其余内容一起被排序。这个函数会保持表头行不变，并允许对输出的其余行进行排序。下面是一些示例，用于说明该函数的用法。

```sh
$ df -h | sort -k 5
/dev/vda2   28G   3.2G  25G       12%  /
tmpfs             504M  68K   504M   1%       /dev/shm
/dev/vda1   485M  444M  17M       97%  /boot
Filesystem  Size  Used  Avail  Use%  Mounted  on
$ df -h | body sort -k 5
Filesystem  Size  Used  Avail  Use%  Mounted  on
/dev/vda2   28G   3.2G  25G       12%  /
tmpfs             504M  68K   504M   1%       /dev/shm
/dev/vda1   485M  444M  17M       97%  /boot
$ ps -eo pid,%cpu,cmd | head -1
  PID %CPU CMD
$ ps -eo pid,%cpu,cmd | sort -nrk2 | head
  675 12.5 mysqld
  PID %CPU CMD
  994  0.0 /usr/sbin/acpid
  963  0.0 /usr/sbin/modem-manager
  958  0.0 NetworkManager
  946  0.0 dbus-daemon
  934  0.0 /usr/sbin/fcoemon --syslog
  931  0.0 [bnx2fc_thread/0]
  930  0.0 [bnx2fc_12_threa]
  929  0.0 [bnx2fc]
$ ps -eo pid,%cpu,cmd | body sort -nrk2 | head
  PID %CPU CMD
  675 12.5 mysqld
  994  0.0 /usr/sbin/acpid
  963  0.0 /usr/sbin/modem-manager
  958  0.0 NetworkManager
  946  0.0 dbus-daemon
  934  0.0 /usr/sbin/fcoemon --syslog
  931  0.0 [bnx2fc_thread/0]
  930  0.0 [bnx2fc_12_threa]
  929  0.0 [bnx2fc]
$
```

### 从字符串或输出行中删除一个字符或一组字符

```sh
$ command | tr -d "X"
$ command | tr -d [SET]
$ cat file | tr -d "X"
$ cat file | tr -d {SET}
```

tr 命令通常用于转换字符，但使用 -d 选项时，它会删除字符。此示例展示了如何去掉引号。

```sh
$ cat cities.csv
1,"Chicago","USA","IL"
2,"Austin","USA","TX"
3,"Santa Cruz","USA","CA"
$ cat cities.csv | cut -d, -f2
"Chicago"
"Austin"
"Santa Cruz"

$ cat cities.csv | cut -d, -f2 | tr -d '"'
Chicago
Austin
Santa Cruz
$
```

你也可以让 tr 删除一组字符。此示例会从输出中删除所有元音字母。

```sh
$ cat cities.csv | cut -d, -f2 | tr -d [aeiou]
"Chcgo"
"Astn"
"Snt Crz"
$
```

### 统计字符串出现次数

```sh
$ uniq -c file
$ command | uniq -c
```

uniq 命令会省略文件中相邻的重复行。由于 uniq 不会检查整个文件或输入流中的唯一行，而只检查相邻的唯一行，因此通常通过管道在其前面接上 sort 命令。你可以使用 "-c" 选项让 uniq 命令统计字符串的唯一出现次数。当你试图在日志文件中查找相同消息、PID、状态码、用户名等的出现次数时，这会很有用。

让我们在名为 access.log 的 Apache Web 服务器日志文件中找出所有唯一的 HTTP 状态码。为此，使用 awk 命令打印日志文件中的第九项。

```sh
$ tail -1 access.log
18.19.20.21 - - [19/Apr/2014:19:51:20 -0400] "GET / HTTP/1.1" 200 7136 "-" "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/33.0.1750.154 Safari/537.36"
$ tail -1 access.log | awk '{print $9}'
200
$ awk '{print $9}' access.log | sort | uniq
200
301
302
404
$
```

我们再进一步，统计每种状态码各有多少。

```sh
$ awk '{print $9}' access.log | sort | uniq -c | sort -nr
5641 200
207 301
86 404
18 302
2 304
```

现在，让我们从 access.log 文件中提取状态码和小时，并统计这些组合的唯一出现次数。接下来，按出现次数对它们排序。这将显示网站最活跃的时段。

```bash
$ cat access.log | awk '{print $9, $4}' | cut -c 14,18-19 | uniq -c | sort -n | tail

      72 200 09
      75 200 06
      81 200 06
      82 200 06
      83 200 06
      83 200 06
      84 200 06
     109 200 20
     122 200 20
     383 200 10
```

## 网络与 SSH

### 通过 Web 界面提供当前目录中的文件

```sh
    $ python -m SimpleHTTPServer
    $ python3 -m http.server
```

默认情况下，此命令会启动一个 Web 服务器，并在 8000 端口上提供当前目录中的内容。你可以通过在该行末尾指定端口来更改端口。如果当前目录中不存在 index.html 文件，则会显示目录列表。启动 Web 服务器，并使用 Web 浏览器访问它。（firefox http://localhost:8000）

当你处理 HTML 内容，并且想在不安装和配置完整 Web 服务器的情况下查看它在 Web 浏览器中的效果时，这会很方便。

```sh
    $ python -m SimpleHTTPServer
    Serving HTTP on 0.0.0.0 port 8000 ...
    localhost.localdomain - - [06/Apr/2014 21:49:20] "GET / HTTP/1.1" 200 -
```




以下介绍如何在标准 HTTP 端口上启动 Web 服务器。由于 80 端口是特权端口，即端口号小于或等于 1024，因此这样做需要 root 权限。

```shell
$ sudo python -m SimpleHTTPServer 80
Serving HTTP on 0.0.0.0 port 80 ...
```

## 通过 SSH 将远程服务器上的目录挂载到本地主机

> 远程目录 / 本地目录

```shell
$ sshfs remote-host:/directory mountpoint
$ fusermount -u mountpoint
```

有时，如果文件和目录位于或看起来位于本机，操作起来会更方便。例如，你可能有一个本地应用程序，而服务器上没有该程序，你用它来操作文件。与其从服务器下载文件、修改后再上传回服务器，不如将远程目录挂载到本地工作站上。下面是一个通过 SSH 更新网站的例子。

```shell
$ mkdir web-files
$ sshfs www.example.com:/home/jason/public_html web-files
$ bluefish web-files/index.html
$ fusermount -u web-files
```

与 ssh 命令一样，如果你的远程用户名与本地用户名不同，可以使用 user@host 格式。另外，如果冒号后未指定目录，则默认使用你的主目录。

## 使用 Curl 从命令行获取公网 IP

```shell
$ curl ifconfig.me
```

如果你需要确定自己的公网（Internet）IP 地址，可以使用 ifconfig.me 网站。

```shell
$ curl ifconfig.me
198.145.20.140

$ curl ifconfig.me/ip
198.145.20.140

$ curl ifconfig.me/host
pub2.kernel.org
```

## 免密码 SSH 登录远程系统

为了免密码 SSH 登录远程主机，你需要一对 SSH 密钥，包括私钥和公钥。在远程主机上，公钥的内容需要放在 ~/.ssh/authorized_keys 中。ssh-copy-id 脚本会完成这项工作。

如果你想生成不带密码的密钥，只需在提示输入密码短语时按回车键即可。你也可以选择为 -N 选项提供空字符串。（ssh-keygen -N ''）

```shell
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/jason/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/jason/.ssh/id_rsa.
Your public key has been saved in /home/jason/.ssh/id_rsa.pub.
The key fingerprint is:
0d:2e:e4:32:dd:da:60:a5:2e:0f:c5:89:d5:78:30:ad jason@laptop.localdomain

The key's randomart image is:
+---[ RSA 2048]----+
|        o.       |
|        =.       |
|        +.=      |
|        BEB o    |
|        + @ S .  |
|        * =      |
|      o o .      |
|        +        |
|        .        |
+-----------------+
$ ssh-copy-id linuxserver
jason@192.168.122.60's password:
Now try logging into the machine, with "ssh 'linuxserver'", and check in:
    .ssh/authorized_keys
to make sure we haven't added extra keys that you weren't expecting.
$ ssh linuxserver
$ hostname
linuxserver
$
```

## 显示打开的网络连接

lsof 命令不仅可以用于显示打开的文件，还可以显示打开的网络端口和网络连接。-P 选项阻止将端口号转换为端口名。-n 选项阻止将 IP 地址转换为主机名。-i 选项告诉 lsof 显示网络连接。

```shell
$ sudo lsof -Pni
COMMAND     PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
dhclient    989 root    6u  IPv4  11522      0t0  UDP *:68
sshd       1202 root    3u  IPv4  12418      0t0  TCP *:22 (LISTEN)
sshd       1202 root    4u  IPv6  12423      0t0  TCP *:22 (LISTEN)
ntpd       1210  ntp   16u  IPv4  12464      0t0  UDP *:123
ntpd       1210  ntp   17u  IPv6  12465      0t0  UDP *:123
ntpd       1210  ntp   18u  IPv4  12476      0t0  UDP 127.0.0.1:123
ntpd       1210  ntp   19u  IPv4  12477      0t0  UDP 192.168.122.60:123
ntpd       1210  ntp   20u  IPv6  12478      0t0  UDP [::1]:123
ntpd       1210  ntp   21u  IPv6  12479      0t0  UDP [fe80::5054:ff:fe52:d858]:123
master      1364  root   12u  IPv4  12761      0t0  TCP 127.0.0.1:25 (LISTEN)
clockd-app  1247  jason 21u  IPv4  78889      0t0  TCP 192.168.122.60:39021->184.25.102.40:80 (ESTABLISHED)
sshd       12339 root   3r  IPv4  74023      0t0  TCP 192.168.122.60:22->192.168.122.1:34483 (ESTABLISHED)
sshd       12342 jason  3u  IPv4  74023      0t0  TCP 192.168.122.60:22->192.168.122.1:34483 (ESTABLISHED)
$
```

## 比较远程文件与本地文件的差异

```shell
$ ssh remote-host cat /path/to/remotefile | diff /path/to/localfile -
```

要显示本地文件与远程文件之间的差异，可以通过 ssh 对文件执行 cat，并将输出通过管道传给 diff 或 sdiff 命令。diff 和 sdiff 命令可以通过为其中一个文件名提供短横线（-）来接受标准输入，以代替文件。

```shell
$ ssh linuxsrv cat /etc/passwd | diff /etc/passwd -
32c32
< terry:x:503:1000::/home/terry:/bin/ksh
---
> terry:x:503:1000::/home/terry:/bin/bash
```

## 创建 SSH 隧道以访问远程资源

```shell
$ ssh -N -L local-port:host:remote-port remote-host
```

要创建 SSH 隧道，请使用 -L 选项。第一个端口是将要在本地机器上打开的端口。发往该端口的连接将通过 remote-host 进行隧道传输，并发送到 -L 选项中指定的主机和远程端口。-N 选项告诉 SSH 不要在远程主机上执行命令——也就是你的 shell。

假设你想访问一个无法在互联网上访问、但可以从你有 SSH 访问权限的服务器上访问的网站。你可以创建一个隧道，让你像在公司防火墙后面一样浏览该网站。以下命令会将本地机器上 8000 端口的连接通过跳板服务器转发到内网服务器的 80 端口。将你的 Web 浏览器指向 http://localhost:8000 并开始浏览。

```shell
$ ssh -N -L 8000:intranet.acme.com:80 jump-server &
[1] 23253
$ firefox http://localhost:8000
```

另一个用例是访问运行在你有 SSH 访问权限的服务器上的服务。如果你需要访问一个只允许来自特定主机的数据库连接的 MySQL 服务器，你可以为你的连接创建 SSH 隧道。由于 MySQL 服务运行在远程机器的 localhost:3306 上，-L 选项应如下所示：-L 3306:localhost:3306。你可以在本地机器上使用 mysql 命令行客户端连接数据库，但更有趣的是使用服务器上没有的图形桌面应用程序。例如，你可以使用此隧道，并通过 MySQL Workbench、Navicat 或其他应用程序连接数据库。

```shell
$ ssh -N -L 3306:localhost:3306 db01 &
[1] 13455

$ mysql -h 127.0.0.1
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 5.1.73 Source distribution
Copyright (c) 2000, 2013, Oracle and/or its affiliates. All rights reserved.
Oracle is a registered trademark of Oracle Corporation and/or its affiliates. Other names may be trademarks of their respective owners.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
mysql>
```

## 查明哪些程序正在监听哪些端口

```shell
$ sudo netstat -nutlp
```

以下是用于获取程序列表及其正在监听的端口的 netstat 选项说明。

- `-n` 显示数字地址，而不是解析符号名称
- `-u` 包含 UDP 协议
- `-t` 包含 TCP 协议
- `-l` 仅显示监听套接字
- `-p` 显示 PID 和程序名

```shell
$ sudo netstat -nutlp
Active Internet connections (only servers)

Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name
tcp        0      0 0.0.0.0:3306         0.0.0.0:*        LISTEN 4546/mysqld
tcp        0      0 0.0.0.0:22           0.0.0.0:*        LISTEN 1161/sshd
tcp        0      0 127.0.0.1:25         0.0.0.0:*        LISTEN 1325/master
tcp        0      0 :::80                :::*             LISTEN 4576/httpd
tcp        0      0 :::22                :::*             LISTEN 1161/sshd
udp        0      0 0.0.0.0:68           0.0.0.0:*        1008/dhclient
$
```

## 为指定远程主机使用不同的 SSH 密钥

将以下内容放入 ~/.ssh/config 文件中。

```text
Host remote-host
IdentityFile ~/.ssh/id_rsa-remote-host
```

如果你需要或想要为不同主机使用不同的 SSH 密钥，可以在命令行中使用 ssh 的 -i 选项显式指定它们。

```shell
$ ssh -i ~/.ssh/id_rsa-db1 db1.example.com
```

如果你想避免每次都指定密钥，可以在 ~/.ssh/config 文件中创建条目并在其中指定密钥。

```shell
$ cat ~/.ssh/config
```




```
Host db1.example.com
    IdentityFile ~/.ssh/id_rsa-db1
$ ssh db1.example.com
```

你可以在主机规范中使用通配符。

```
$ cat ~/.ssh/config
Host db*
    IdentityFile ~/.ssh/id_rsa-db1
Host *.work.net
    IdentityFile ~/work-files/keys/id_rsa
$ ssh jim@jumpbox.work.net
```

如果你根据相关主机的完全限定域名来命名 SSH 密钥，就可以使用 %h 转义字符来简化你的 ~/.ssh/config 文件。%h 语法会展开为你正在连接的主机的完全限定域名，而无需为每台服务器单独设置一个主机条目。

```
$ cat ~/.ssh/config
Host *.example.com
    IdentityFile ~/.ssh/id_rsa-%h
$ ls -l ~/.ssh/id_rsa-*
id_rsa-lax-db-01.example.com
id_rsa-lax-db-01.example.com.pub
id_rsa-lax-web-01.example.com
id_rsa-lax-web-01.example.com.pub
$ ssh lax-db-01.example.com
```

## 避免在通过 SSH 连接时输入用户名

将以下内容放入 `~/.ssh/config` 文件中。

```
Host remote-host
User username
```

如果你本地 Linux 机器上的用户名与远程 Linux 机器上的用户名不同，则在通过 SSH 连接时必须指定用户名。如下所示：

```
$ ssh jim@server1.example.com
```

为了避免每次都输入 “username@”，请在你的 `~/.ssh/config` 文件中添加一个主机条目。

```
Host server1.example.com
        User jim
```

配置好主机条目后，你就可以直接通过 ssh 连接远程主机了。

```
$ whoami
james
$ ssh server1.example.com
$ whoami
jim
$
```

## 简化多跳 SSH 连接并透明代理 SSH 连接

将以下内容放入 ~/.ssh/config 文件中。

```
Host jumphost.example.com
    ProxyCommand none
Host *.example.com
    ProxyCommand ssh -W %h:%p jumphost.example.com
```

如果你需要访问位于 SSH 网关服务器或跳板服务器后面的主机，你可以通过让 SSH 在连接最终远程主机时自动使用该 SSH 网关来让生活更轻松。无需先连接网关，再输入另一条 ssh 命令来连接目标主机，你只需在本地机器上输入 “ssh destination-host”。使用上述配置，此命令会将你对 server1 的 ssh 连接通过 jumphost 进行代理。

```
$ ssh server1.example.com
$ uname -n
server1
$
```

## 断开远程会话并稍后重新连接，接续之前的工作

```
$ ssh remote-host
$ screen
ctrl-a d
$ exit
```

```bash
$ ssh remote-host
$ screen -r
```

当我在远程主机上需要完成一个长时间运行的进程时，我总是在启动该进程之前先启动一个 screen 会话。我不希望网络连接中的任何小故障打断远程主机上正在执行的工作。有时我会启动一个进程，从会话中分离，稍后再重新连接以查看我离开期间产生的所有输出。

首先，通过 ssh 连接到远程主机。接下来，启动一个 screen 会话。开始在远程主机上执行你的工作。通过输入 ctrl-a 然后按 d 来从 screen 会话中分离。你启动的进程在你离开期间仍会在 screen 会话中继续运行。此外，产生的任何输出都可以在之后供你查看。

```text
$ ssh remote-host
$ screen
$ /usr/local/bin/migrate-db

Starting DB migration at Sun Apr 13 21:02:50 EDT 2014
<ctrl-a,d>
[detached]
$ exit
```

要重新连接到你的 screen 会话，请连接到远程主机并输入 screen -r。如果有任何输出滚过了屏幕顶部，你可以通过输入 ctrl-a 然后按 Esc 键来查看。现在使用 vi 导航键绑定来查看输出历史。例如，你可以按 k 向上移动一行，或按 ctrl-b 向上翻页。查看完输出历史后，按 Esc 键返回到实时会话。要退出你的 screen 会话，输入 exit。

```shell
$ ssh remote-host
$ screen -r
Starting DB migration at 21:02
table1 migrated at 21:34
table2 migrated at 22:11
table3 migrated at 22:54
DB migration completed at 23:04
$ exit
[screen is terminating]
$ exit
```

Screen 是使用最广泛、最容易获得的屏幕复用器之一。不过，也有其他替代品，如 tmux、dtach 和 byobu。

## 配置 SSH 根据模式将域名附加到主机名

~/.ssh/config 的内容：

```ssh
host-prefix* !*.domain.com
        HostName %h.domain.com
```

如果你通过 ssh 连接到多个域中的主机，每次都输入完全限定域名会变得很烦人。解决这个问题的一种方法是将每个域添加到 /etc/resolv.conf 的搜索列表中。解析器会尝试在搜索列表中的每个域中解析指定的主机名，直到找到能够解析的域为止。

```shell
$ cat /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4
search domain1.com domain2.com domain3.com domain4.com domain5.com domain6.com domain7.com
```

使用上述 resolv.conf，当你输入 “ssh remote-host” 时，解析器将尝试将 remote-host.domain1.com 转换为 IP 地址。如果失败，则会尝试解析 remote-host.domain2.com，依此类推。上述 resolv.conf 的问题在于搜索列表仅限于六个域。因此，remote-host.domain7.com 永远不会被尝试。此外，搜索列表长度限制为 256 个字符，无论域的数量有多少。

如何绕过六个域的搜索列表限制？如果你足够幸运，主机名与域名之间存在某种关联模式，你可以配置 ssh 来执行解析。例如，对于像 “ny-www1.newyork.company.com” 和 “ny-mysql-07.newyork.company.com” 这样的完全限定域名，你可以创建一条规则，将 “.newyork.company.com” 附加到任何以 “ny” 开头的主机名上。你还需要告诉 ssh 忽略那些以 “ny” 开头但已经带有 “.newyork.company.com” 后缀的主机。下面是一个实现此功能的 ~/.ssh/config 示例文件。

```text
$ cat ~/.ssh/config

ny* !*.newyork.company.com
        HostName %h.newyork.company.com

db* !*.databases.company.com
        HostName %h.databases.company.com

jump* !*.company.com
        HostName %h.company.com
```

现在，当你输入 “ssh ny-test” 时，ssh 将尝试连接到 “ny-test.newyork.company.com”。对于以 “db” 开头的主机，ssh 会将 “.databases.company.com” 附加到主机名上。以 “jump” 开头的主机，则会在其后附加 “.company.com” 域名。

```shell
$ ssh ny-www1
$ hostname -f
ny-www1.newyork.company.com
$ exit
$ ssh jump-ny-01
$ hostname -f
jump-ny-01.company.com
$ exit
$
```

## 运行不受挂断影响的命令，让你断开连接后任务仍能继续运行

```shell
$ nohup command &
```

通常，当你在后台启动一个任务并注销会话时，该任务会被终止。确保命令在你断开与主机的连接后继续运行的一种方法是使用 nohup 命令。Nohup 代表 no hang up（不挂断）。默认情况下，命令的输出会存储在程序启动目录下的一个名为 “nohup.out” 的文件中。你可以在之后查看该文件的内容来了解命令的输出。如果想使用不同的文件名，可以使用重定向。

```shell
$ ssh db-server
$ nohup /usr/local/bin/upgradedb.sh &
[1] 13370

$ exit
$ ssh db-server
$ cat nohup.out
Starting database upgrade.
...
Database upgrade complete.
$ nohup /usr/local/bin/post-upgrade.sh > /tmp/post.log &
[1] 16711

$ exit
$ ssh db-server
$ cat /tmp/post.log
Post processing completed.
$
```

## 使用 SSH SOCKS 代理加密你的网页浏览数据

```shell
$ ssh -D PORT remote-host
```

如果你正在使用开放的无线热点，并希望确保网页浏览数据被加密，你可以通过 SSH 将网页浏览流量重定向到另一台主机。使用 ssh 的 “-D” 选项，并提供一个在你本地计算机上打开的端口用于代理连接。如果你只想进行端口转发而不实际登录远程主机的 shell，请使用 ssh 的 “-N” 选项。将你的 Web 浏览器配置为使用 SOCKS 5 代理，主机名使用 localhost，端口使用你提供给 ssh 的端口。





```bash
$ ssh -ND 1080 ubuntu@ec2-75-101-157-145.compute-1.amazonaws.com
$ firefox http://www.mybank.com
```

## 从命令行下载网页、HTTP 数据或使用 Web API

```bash
$ curl -o file.html http://website/webpage
$ wget http://website/webpage
```

`curl` 和 `wget` 命令可用于下载网页或 Web 服务器上可用的任何内容。你可以使用这些命令与 HTTP API 交互、下载软件包、下载状态页面，甚至获取当前天气。

下面是一个检查本地 Apache Web 服务器状态页面的示例。

```text
$ curl -o server-status.html http://localhost/server-status

 % Total    % Received % Xferd  Average Speed
Time      Time     Time  Current
                              Dload  Upload
Total   Spent      Left  Speed
100  6148  100  6148    0     0   1070k
0     0     --:--:--  --:--:--  --:--:--  1200k
$ wget http://localhost/server-status

--2014-04-19 14:37:18--  http://localhost/server-status
Resolving localhost (localhost)... 127.0.0.1
Connecting to localhost (localhost)|127.0.0.1|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 6377 (6.2K) [text/html]
Saving to: ‘server-status’
100%[=====>] 6,377 --.-K/s in 0s
2014-04-19 14:37:18 (105 MB/s) - ‘server-status’ saved [6377/6377]
$ grep uptime server-status*
server-status:<dt>Server uptime: 50 minutes 13 seconds</dt>
server-status.html:<dt>Server uptime: 50 minutes 5 seconds</dt>
```

下面是一个获取当前天气的示例。

```text
$ curl -so lax-weather.html \
http://weather.noaa.gov/pub/data/observations/metar/decoded/KLAX.TXT
$ cat lax-weather.html
LOS ANGELES INTL AIRPORT, CA, United States
(KLAX) 33-56N 118-23W 46M
Apr 19, 2014 - 02:53 PM EDT / 2014.04.19 1853 UTC
Wind: from the W (260 degrees) at 10 MPH (9 KT):0
Visibility: 10 mile(s):0
Sky conditions: mostly cloudy
Temperature: 64.9 F (18.3 C)
Dew Point: 54.0 F (12.2 C)
Relative Humidity: 67%
Pressure (altimeter): 30.03 in. Hg (1016 hPa)
ob: KLAX 191853Z 26009KT 10SM FEW022 BKN220 18/12 A3003 RMK AO2 SLP167 T01830122
cycle: 19
$ wget -q \
http://weather.noaa.gov/pub/data/observations/metar/decoded/KLAX.TXT
$ cat KLAX.TXT
LOS ANGELES INTERNTL AIRPORT, CA, United States
(KLAX) 33-56N 118-23W 46M
Apr 19, 2014 – 02:53 PM EDT / 2014.04.19 1853 UTC
Wind: from the W (260 degrees) at 10 MPH (9 KT):0
Visibility: 10 mile(s):0
Sky conditions: mostly cloudy
Temperature: 64.9 F (18.3 C)
Dew Point: 54.0 F (12.2 C)
Relative Humidity: 67%
Pressure (altimeter): 30.03 in. Hg (1016 hPa)
ob: KLAX 191853Z 26009KT 10SM FEW022 BKN220 18/12 A3003 RMK AO2 SLP167 T01830122
cycle: 19
$
```

下载并安装一个软件包。

```text
$ wget -q \
https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.1.1.deb
$ sudo dpkg -i elasticsearch-1.1.1.deb
Selecting previously unselected package elasticsearch.
(Reading database ... 162097 files and directories currently installed.)
Unpacking elasticsearch (from elasticsearch-1.1.1.deb) ...
Setting up elasticsearch (1.1.1) ...
Adding system user `elasticsearch' (UID 116) ...
Adding new user `elasticsearch' (UID 116) with group `elasticsearch' ...
Not creating home directory `/usr/share/elasticsearch'.
### NOT starting elasticsearch by default on bootup, please execute
  sudo update-rc.d elasticsearch defaults 95 10
### In order to start elasticsearch, execute
  sudo /etc/init.d/elasticsearch start
Processing triggers for ureadahead ...
$ sudo /etc/init.d/elasticsearch start
 * Starting Elasticsearch Server
[ OK ]
$
```

与 Web API 交互。

```text
$ curl http://localhost:9200
{
  "status" : 200,
  "name" : "NFL Superpro",
  "version" : {
    "number" : "1.1.1",
    "build_hash" : "f1585f096d3f3985e73456dcc",
    "build_timestamp" : "2014-04-16T14:27:12Z",
    "build_snapshot" : false,
```

## 在命令行使用 for 循环

```bash
$ for VAR in LIST
> do
>   # use $VAR
> done
```

当你需要对一组元素执行相同操作时，可以直接在 shell 中使用 for 循环。

```text
$ for USER in bob jill fred
> do
>   sudo passwd -l $USER
>   logger -t naughty-user $USER
> done
Locking password for user bob.
passwd: Success
Locking password for user jill.
passwd: Success
Locking password for user fred.
passwd: Success
$ sudo tail -3 /var/log/messages
Apr  8 19:29:03 linuxserver naughty-user: bob
Apr  8 19:29:03 linuxserver naughty-user: jill
Apr  8 19:29:03 linuxserver naughty-user: fred
```

你也可以在一行命令行中写完整个循环。

```text
$ for USER in bob jill fred; do sudo passwd -l $USER; logger -t naughty-user $USER; done
...
```

## 命令替换

```bash
$ VAR=`command`
$ VAR=$(command)
```

命令替换有两种形式。第一种形式使用反引号（\`）将命令括起来，第二种形式使用美元符号后跟括号将命令括起来。它们在功能上是等价的，反引号形式是较旧的风格。命令的输出可以用作另一个命令的参数、设置变量，或用于生成 for 循环的参数列表。

```text
$ EXT_FILESYSTEMS=$(grep ext fstab | awk '{print $2}')
$ echo $EXT_FILESYSTEMS
/ /boot
$ cp file.txt file.txt.`date +%F`
$ ls file.txt*
file.txt file.txt.2014-04-08
$ ps -pf $(cat /var/run/ntpd.pid)
UID        PID  PPID  C STIME TTY          TIME CMD
ntp       1210     1  0 Apr06 ?        00:00:05 ntpd -u ntp:ntp -p /var/run/ntpd
$ sudo kill -9 $(cat /var/run/ntpd.pid)
$ for x in $(cut -d: -f1 /etc/passwd); do groups $x; done
jason : jason sales
bobdjr : sales
jim : jim
```

## 将命令行输出存储为变量以供后续使用

```bash
$ for VAR in LIST
> do
>   VAR2=$(command)
>   VAR3=$(command)
>   echo "$VAR2 $VAR3"
> done
```

命令替换可用于为变量赋值。如果你需要多次复用某条命令的输出，可以将其一次性赋值给一个变量，然后重复使用该变量。以下示例演示了如何在同一个脚本中多次使用 id 命令的输出。

```text
$ for USER in $(cut -f1 -d: /etc/passwd)
> do
>   UID_MIN=$(grep ^UID_MIN /etc/login.defs | awk '{print $NF}')
>   USERID=$(id -u $USER)
>   [ $USERID -lt $UID_MIN ] || {
>     echo "Forcing password expiration for $USER with UID of $USERID."
>     sudo passwd -e $USER
> }
> done
Forcing password expiration for bob with UID of 1000.
Forcing password expiration for bobdjr with UID of 1001.
Forcing password expiration for bobbi with UID of 1002.
```

## 逐行读取输入

```bash
$ while read LINE
> do
>   # Do something with $LINE
> done < file.txt

$ command | while read LINE
> do
>   # Do something with $LINE
> done
```

如果要遍历单词列表，请使用 for 循环。如果要逐行遍历，请将 while 循环与 read 语句和重定向结合使用。

让我们查找已使用超过 90% 的文件系统。如果我们尝试使用 if 语句，它会将输出拆分为单词块，如下所示。

```text
$ df | head -1
Filesystem 1K-blocks Used Available Use% Mounted on
$ for x in $(df)
> do
> echo $x
> done
Filesystem
1K-blocks
Used
Available
Use%
Mounted
on
>...
```

我们需要像这样一次读取整行。

```text
$ df | while read LINE
> do
> echo $LINE
> done
Filesystem 1K-blocks Used Available Use% Mounted on
>...
```

下面是一种查找已使用超过 90% 的文件系统的方法。

## 命令行功夫

```bash
$ read -n 1 VAR
$ read -p "Prompt text" VAR
```

要接受用户输入，请使用 read 命令。read 会接受一整行输入并将其存储到变量中。你可以使用 -n 选项强制 read 只读取有限数量的字符。与其在 read 命令之前使用 echo 语句，不如使用 -p 选项提供提示符。下面是一个使用这些技术的示例脚本。

backup.sh 的内容：

```bash
#!/bin/bash
while true
do
    read -p "What server would you like to backup? " SERVER
    echo "Backing up $SERVER"
    /usr/local/bin/backup $SERVER
    read -p "Backup another server? (Y/n) " -n 1 BACKUP_AGAIN
    echo
    [ "$BACKUP_AGAIN" = "y" ] || break
done
```

```text
$ ./backup.sh
What server would you like to backup? thor
Backing up thor
Backup another server? (Y/n) y
```



```text
What server would you like to backup? loki
Backing up loki
Backup another server? (y/n) n
$
```

## 对文本中给定列的所有数字求和

```sh
$ awk '{ sum += $1 } END { print sum }' file
$ cat file | awk '{ sum += $1 } END { print sum }'
```

Awk 可用于汇总一列数值。例如，你可以用这个技巧把给定系统上所有文件系统使用的磁盘空间加起来。

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

## 自动对任何命令回答 Yes

```bash
$ yes | command
$ yes "string" | command
```

如果你要自动化一个需要用户输入的流程，可以看看 yes 命令。默认情况下，yes 只会不断输出 "y"，直到被终止。你可以让 yes 重复任意字符串。如果你想自动回答 "no"，可以运行 "yes no"。

```bash
$ ./install-my-app.sh
Are you sure you want to install my-app? (y/n) y
Ok, my-app installed.
$ yes | ./install-my-app.sh
Ok, my-app installed.
$
```

## 以表格格式显示已挂载的文件系统

```bash
$ mount | column -t
```

mount 命令的输出格式并不易于阅读。要让各列对齐，可将 mount 命令的输出通过管道传给 "column -t"。默认情况下，mount 会显示所有已挂载的文件系统，甚至包括 /proc 和 /sys 之类的伪文件系统。要将输出限制为某种文件系统类型，请使用 -t 选项并提供类型。

```bash
$ mount -t ext4
/dev/mapper/sys-lv_root on / type ext4 (rw)
/dev/sda1 on /boot type ext4 (rw)
$ mount -t ext4 | column -t
/dev/mapper/sys-lv_root on /      type ext4 (rw)
/dev/sda1                  on /boot type ext4 (rw)
```

## 终止指定用户或程序的所有进程

```bash
$ pkill -9 command
$ pkill -u user command
```

如果你需要用同一个命令终止多个进程，请使用 `pkill` 命令。如果你只想终止某个指定用户的进程，请使用 `-u` 选项。Pkill 只有在所有条件都匹配时才会终止进程。这意味着你可以终止某个特定用户正在运行的所有指定进程。

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

## 重复执行命令直到成功

```bash
$ while true
> do
>   command && break
> done
```

while 循环会一直继续，直到条件为假或遇到 break。在这种情况下，我们实际上创建了一个无限循环，并在所选命令成功后跳出。如果你想持续 ping 一台主机直到它响应，就可以使用这个 while 循环。

```bash
$ while true
> do
>     ping -c1 -W1 remote-host >/dev/null 2>&1 && break
> done ; echo "Remote-host is up at $(date)."
Remote-host is up at Fri Apr 11 21:30:29 EDT 2014.
$
```

如果你在等待某个文件出现在服务器上，也可以使用这个 while 循环。

```bash
$ while true
> do
>     ls /srv/ftp/incoming/payroll.txt.gif 2>/dev/null && break
> done; echo "Payroll file arrived at $(date)."
Payroll file arrived at Fri Apr 11 21:33:23 EDT 2014.
```

## 查找谁占用了最多磁盘空间

```bash
$ sudo du -s /home/* | sort -n
```

这个命令会显示在其主目录中占用磁盘空间最多的人。占用磁盘空间少的用户会显示在屏幕顶部，而占用磁盘空间最多的用户会显示在底部。

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

如果你想要更图形化的方式来显示磁盘使用情况，可以试试简洁实用的 ncdu 工具。

```text
$ ncdu /home
ncdu 1.10 ~ Use the arrow keys to navigate, press ? for help
--- /home ---------------------------------------------
37.9GiB [##########] /ryan
 1.3MiB [          ] /lucas
Total disk usage: 37.9GiB  Apparent size: 37.8GiB
Items: 156055
```

## 查找占用磁盘空间最多的文件

```shell
$ find / -type f -exec wc -c {} \; | sort -n
```

使用 find 对每个文件执行 "wc -c" 命令，显示其字节大小，然后对该输出进行排序。最小的文件会先显示，最大的文件会最后显示。如果你要扫描系统上的每个文件，这个命令可能需要一段时间才能完成。

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

## 列出进程，按内存使用量排序

```bash
$ ps aux | sort -nk 4
```

使用这个命令可以找出占用内存最多的进程。占用内存最少的进程会滚出屏幕顶部，而占用内存最多的进程会正好显示在 shell 提示符上方。

在这个示例中，mysql 占用了此主机 1.3% 的内存。

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

## 列出进程，按 CPU 使用率排序

```shell
$ ps aux | sort -nk 3
```

使用这个命令可以找出占用 CPU 最多的进程。占用 CPU 最少的进程会滚出屏幕顶部，而占用 CPU 最多的进程会正好显示在 shell 提示符上方。

在这个示例中，mysqld 占用了此主机 94% 的 CPU。

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





```text
mysql 4447 94 12.8 2134672 1031064 ?  Sl  10:52
27:39 /usr/libexec/mysqld
$
```

## 快速判断你的系统是 32 位还是 64 位

```bash
$ getconf LONG_BIT
```

如果你在某个系统上需要知道它是 32 位还是 64 位，可以使用 getconf。

```bash
$ getconf LONG_BIT
32
$ ssh remote-host getconf LONG_BIT
64
```

## 生成随机密码

```bash
$ openssl rand -base64 48 | cut -c1-PASSWORD_LENGTH
$ gpw () { openssl rand -base64 48 | cut -c1-${1}; }
```

你可以使用 openssl 命令生成随机密码。如果你经常需要这样做，可以创建一个函数，只需传入你想要的密码长度即可。

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

## 文件和目录

### 快速备份文件

```bash
$ cp file{,.bak}
```

你可以使用花括号展开（brace expansion）快速创建文件的备份副本。花括号展开允许你从单个参数创建多个命令行参数。该单个参数会与花括号内给出的所有字符串组合，并生成与花括号字符串数量相同的新参数。花括号中的值可以是逗号分隔的字符串，也可以是序列表达式。序列表达式的例子包括 {1..5} 和 {a..z}。

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

### 快速更改文件扩展名

```bash
$ mv file.old{,.new}
```

要使用新扩展名重命名文件，可以采用花括号展开。这个例子将 ".txt" 文件改为 ".doc" 文件。

```bash
$ ls report*
report.txt
$ mv report.{txt,doc}
$ ls report*
report.doc
$
```

下面是另一个例子。

```bash
$ ls httpd*
httpd.cfg
$ mv httpd.{cfg,conf}
$ ls httpd*
httpd.conf
$
```

这条命令会给文件添加一个扩展名。

```bash
$ ls jazz*
jazz
$ mv jazz{,.mp3}
$ ls jazz*
jazz.mp3
$
```

### 按日期轻松创建文件备份

```bash
$ alias d='date +%F'
```

通过在文件或目录名中使用 YYYY-MM-DD 的日期格式，你可以让 ls 的输出更易于人类阅读。使用这种格式时，你可以快速分辨文件的日期顺序。

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

在修改文件之前，我喜欢先做一份备份副本。我也想知道备份是什么时候做的。通过创建一个别名 "d"（即 YYYY-MM-DD 格式日期的缩写），我可以快速创建这类备份。

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

### 覆盖文件内容

```bash
$ command > file
```

你可以使用大于号将命令输出重定向到文件。单个大于号（>）将标准输出重定向到文件，并覆盖（截断）文件中已有的任何内容。如果文件不存在，则会创建一个。

```bash
$ grep bash /etc/passwd > users-that-use-bash
$ cat users-that-use-bash
root:x:0:0:root:/root:/bin/bash
jason:x:501:501:Jason:/home/jason:/bin/bash
oracle:x:1006:1006::/home/oracle:/bin/bash
bob:x:1000:1000:Bob Smith:/home/bob:/bin/bash
$
```

### 清空正在被写入的文件

```bash
$ > file
$ cat /dev/null > file
```

要快速将文件清零，你可以将“无内容”重定向到该文件。为什么不直接删除文件再重新创建呢？因为如果一个进程在文件被删除时仍打开着它，该进程会保持文件句柄打开并继续写入该文件。只有当进程关闭文件句柄时，该文件占用的磁盘空间才会被释放。如果应用程序把 /var 填满了，而你删除了正在打开的日志文件，/var 仍然会是满的。如果你将“无内容”重定向到文件，文件会被截断，应用程序也能继续写入该文件。

```bash
$ sudo -s
# > /var/log/maillog
# ls -l maillog

-rw-------. 1 root root 0 Apr 9 18:55 maillog
```

### 向文件追加字符串

```bash
$ command >> file
```

双大于号（>>）将标准输出重定向到文件，并追加到已有的任何内容之后。如果文件不存在，则会创建一个。

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

### 实时跟踪文件增长

```bash
$ tail -f file
```

对于像日志文件这样不断更新的文件，可以使用 tail -f 实时查看文件的更新内容。

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

### 同时查看多个日志文件

```bash
$ multitail file1 fileN
$ multitail file1 -I fileN
```

multitail 命令允许你同时浏览多个文件。multitail 不仅可以同时查看多个文件，还支持颜色高亮、过滤、合并等功能。下面是一些最有用的 multitail 命令的快速介绍。

- F1 - 帮助
- a - 添加另一个要跟踪的文件
- d - 从视图中删除一个文件
- / - 开始搜索（查找）
- ctrl-g - 编辑命令、菜单或操作。类似于 emacs 的 ctrl-g 键绑定。
- q - 退出

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

要将多个文件合并到一个窗口中，可以使用 "-I" 选项。这会将两个文件的输出混合在一起，有助于排查问题。

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


```text
001] /var/log/syslog *Press F1/<CTRL>+<h> for help*
132KB - 2014/04/19 12:48:32
```

## 删除空目录

```bash
$ find . -type d -empty -delete
```

如果你发现自己需要清理空目录，find 可以让这项任务变得轻而易举。使用 -type d 选项查找所有目录，使用 -empty 选项仅包含空目录，最后使用 -delete 选项删除这些目录。

```bash
$ mkdir -p testing/{1..4}
$ ls testing/
1  2  3  4
$ find . -type d -empty -delete
$ ls testing/
ls: cannot access testing/: No such file or directory
$
```

## 打印包含给定字符串的文件列表

```bash
$ grep -rl string .
```

要获取包含给定字符串的文件列表，请使用 grep 的 -r（递归）和 -l（列出匹配文件）选项。

```bash
$ sudo grep -lr jim /var/log
/var/log/audit/audit.log.1
/var/log/secure-20140406
/var/log/secure
```

## 易于阅读的递归文件列表

```bash
$ find . -type f -ls
```

ls 命令有一个递归选项，但我发现 find 命令的输出更易于理解，尤其是在文件和目录数量很多时。使用 find 的优势在于它会显示每个文件的完整路径，而 ls 不会。

```text
$ ls -lR Music/
Music/:
total 4
drwxr-xr-x. 2 jason jason 4096 Feb 22 12:40 jazz
Music/jazz:
total 20932
-rw-r--r--. 1 jason jason       79496 Feb 22 12:40 giant-steps.mp3
-rw-r--r--. 1 jason jason 21267371 Feb 16 11:12 jazz-album-1.mp3
-rw-r--r--. 1 jason jason       79496 Feb  3 18:13 john-coltrane.mp3
$ find Music/ -type f -ls
397966 20772 -rw-r--r--   1 jason jason 21267371 Feb
16 11:12 Music/jazz/jazz-album-1.mp3
396787    80 -rw-r--r--   1 jason jason    79496 Feb 22
12:40 Music/jazz/giant-steps.mp3
132464    80 -rw-r--r--   1 jason jason    79496 Feb  3
18:13 Music/jazz/john-coltrane.mp3
$
```

## 以树形格式查看文件和目录

```bash
$ tree
$ tree -d
$ tree -L number
```

tree 命令以类似树形的格式显示文件和目录。如果你只想查看目录结构，请使用 -d 选项。要限制树的深度，请使用 -L 选项，后跟一个数字。

```text
$ tree Music/
Music/
└── jazz
    ├── giant-steps.mp3
    ├── jazz-album-1.mp3
    └── john-coltrane.mp3
1 directory, 3 files
$ tree -d Music/
Music/
└── jazz
1 directory
$ tree -d /var | head
/var
├── account
├── cache
│   ├── fontconfig
│   ├── gdm
│   │   ├── adminuser
│   │   └── jason
├── hald
├── ldconfig
├── man
$ tree -dL 1 /var
/var
├── account
├── cache
├── crash
├── db
├── empty
├── ftp
├── games
├── gdm
├── lib
├── local
├── lock
├── log
├── mail -> spool/mail
├── nis
├── opt
├── preserve
├── run
├── spool
├── tmp
├── www
└── yp
$
```

## 在多个文件中替换字符串

```bash
$ find /path -type f -exec sed -i.bak 's/string/replacement/g' {} \;
```

如果你有一些信息嵌入在多个文件中，并且需要更改它，请将 find 命令与 sed 结合使用。sed 的 -i 选项告诉它执行原地编辑。你可以为 -i 提供一个扩展名，以便在编辑之前创建文件备份。传递给 sed 的命令告诉它全局用 "replacement" 替换 "string"。全局替换会在所有位置执行替换。普通替换只替换一行中的第一个匹配项。

在此示例中，托管软件仓库的服务器正在被替换。使用下面的一行命令，所有出现的 "thor" 都会被替换为 "loki"。

```text
$ grep -r thor .
./deploy-il.sh:REPO_SERVER="thor.company.com"
./deploy-ca.sh:REPO_SERVER="thor.company.com"
./deploy-fl.sh:REPO_SERVER="thor.company.com"
./deploy-ny.sh:REPO_SERVER="thor.company.com"

$ find . -type f -exec sed -i.bak 's/thor/loki/g' {} \;
$ grep -r thor .
./deploy-fl.sh.bak:REPO_SERVER="thor.company.com"
./deploy-il.sh.bak:REPO_SERVER="thor.company.com"
./deploy-ny.sh.bak:REPO_SERVER="thor.company.com"
./deploy-ca.sh.bak:REPO_SERVER="thor.company.com"
$ grep -r loki .
./deploy-il.sh:REPO_SERVER="loki.company.com"
./deploy-ca.sh:REPO_SERVER="loki.company.com"
./deploy-fl.sh:REPO_SERVER="loki.company.com"
./deploy-ny.sh:REPO_SERVER="loki.company.com"
$
```

## 从文件中提取第 N 行

```bash
$ awk 'NR==N'
```

要从文件中提取特定行，请告诉 awk 打印与行号匹配的行。一个有用的场景是当你在脚本中遇到错误时。要确切查看脚本在该行执行什么，请使用 awk。

```text
$ ./deploy.sh
./deploy.sh: line 74: /usr/local/bin/patch: No such
file or directory
$ awk 'NR==74' deploy.sh
/usr/local/bin/patch $NEW_HOST
$
```

## 将文本文件从 Windows 格式转换为 Linux 格式，反之亦然

```bash
$ dos2unix
$ unix2dos
```

迟早你会收到或下载一个使用 CR（回车）和 LF（换行）字符对来终止文件中各行的文件。这类文件是 Windows/DOS 格式的。类 Unix 操作系统仅使用 LF 字符来终止一行。有时这会导致问题。要将文件转换为类 Unix 格式，请使用 dos2unix。要检查行终止字符，请使用 "cat -A" 或 "file" 命令。

```text
$ cat -A from-my-windows-buddy.pl
#!/usr/bin/perl^M$
print "This is a cross-platform perl script!\n"^M$
$ ./from-my-windows-buddy.pl
-bash: ./from-my-windows-buddy.pl: /usr/bin/perl^M:
bad interpreter: No such file or directory
$ dos2unix from-my-windows-buddy.pl
dos2unix: converting file from-my-windows-buddy.pl to
UNIX format ...
$ cat -A from-my-windows-buddy.pl
#!/usr/bin/perl$
print "This is a cross-platform perl script!\n"$
$ ./from-my-windows-buddy.pl
This is a cross-platform perl script!
$ file other-file.txt
other-file.txt: ASCII text, with CRLF line
terminators
$ dos2unix other-file.txt
dos2unix: converting file other-file.txt to UNIX
format ...
$ file other-file.txt
other-file.txt: ASCII text
$
```

另一方面，如果你将在 Linux 主机上创建的文件发送给在 Windows 的记事本中打开它的人，他们只会看到一整行很长的文本。使用 unix2dos 命令将文件转换为 Windows/DOS 格式。

```text
$ file report-for-ceo.txt
report-for-ceo.txt: ASCII text

$ unix2dos report-for-ceo.txt
unix2dos: converting file report-for-ceo.txt to DOS
format ...

$ file report-for-ceo.txt
report-for-ceo.txt: ASCII text, with CRLF line
terminators
$
```

## 杂项

### 切换到上一个工作目录

```bash
$ cd -
```

如果你想返回上一个工作目录，请使用 "cd -"。OLDPWD 环境变量保存你最近一次目录位置的路径。"cd -" 与 "cd $OLDPWD" 相同。

```text
$ cd /etc/httpd/conf.d
$ grep ^SSLCert ssl.conf
SSLCertificateFile /etc/pki/tls/certs/localhost.crt
SSLCertificateKeyFile
/etc/pki/tls/private/localhost.key
$ cd /etc/pki/tls/certs/
$ ls
ca-bundle.crt  ca-bundle.trust.crt  localhost.crt
make-dummy-cert  Makefile  renew-dummy-cert
$ cd -
/etc/httpd/conf.d
```

### 重置终端模拟器显示

```text
$ reset
```

将二进制文件显示到屏幕上可能会导致终端变得不可用。要尝试恢复，请输入 "reset" 并按回车。你的终端可能处于这样一种状态：你看不到自己正在输入的内容，但 shell 仍会接受输入。

```text
$ cat blue-train.mp3
F...A....h...reset
$ 
```

### 从命令行搜索 Wikipedia

```bash
$ dig +short txt <string>.wp.dg.cx
$ host -t txt <string>.wp.dg.cx
```

如果你需要快速查找某个主题的一些信息，可以使用 DNS 搜索 Wikipedia。名称服务器会以 TXT 记录的形式返回 Wikipedia 文章摘要。

```text
$ dig +short txt linux.wp.dg.cx
"Linux is a Unix-like computer operating system
assembled under the model of free and open source
software development and distribution. The defining
component of Linux is the Linux kernel, an operating
system kernel first released 5 October 1991 by Linus
Torvalds, http://en.wikipedia.org/wiki/Linux"
$ host -t txt bash_shell.wp.dg.cx
bash_shell.wp.dg.cx descriptive text "Bash is a Unix
```





> 由 Brian Fox 为 GNU 项目编写的 shell，作为
> Bourne shell（sh）的自由软件替代品。Bash 是一个命令处理器，通常在
> 文本窗口中运行，允许用户输入命令来
> 触发操作。Bash 还可以从
> 一个称为脚本的文件中读取命令。像所有 Unix shell 一样，它
> 支持文件名通配、管道、here
> 文档……
> http://en.wikipedia.org/wiki/Bash_(Unix_shell)"

你可以创建一个小型 shell 脚本，以免每次都要输入完整的 DNS 查询。

```bash
$ echo -e '#!/bin/bash\ndig +short txt ${1}.wp.dg.cx' > wikidig
$ chmod 755 !$
chmod 755 wikidig
$ ./wikidig ubuntu_operating_system
```

> “Ubuntu 截至 2012 年，根据在线调查，
> Ubuntu 是台式机/笔记本电脑个人电脑上最受欢迎的 Linux 发行版，而且大多数 Ubuntu
> 报道都聚焦于它在该市场中的使用。然而，
> 它在服务器和云计算领域也很受欢迎。
> http://en.wikipedia.org/wiki/Ubuntu_(operating_system)"

或者，你也可以改为创建一个函数，并将其添加到你的 dot 文件中。

```bash
$ echo 'wikidig() { dig +short txt ${1}.wp.dg.cx; }' >> .bash_profile
$ . ~/.bash_profile
$ wikidig jazz
"Jazz is a musical style that originated at the
beginning of the 20th century in black communities in
the Southern United States. It was born out of a mix
of African and European music traditions. Its African
pedigree is evident in its use of blue notes,
improvisation, polyrhythms, syncopation and the swung
note. From its early development until the present
day jazz has also...
http://en.wikipedia.org/wiki/Jazz"
```

## 让非交互式 Shell 会话与交互式会话行为一致

在 ~/.bashrc 中进行任何自定义。~/.bash_profile 的内容如下：

```bash
if [ -f ~/.bashrc ]; then
source ~/.bashrc
fi
```

当你以交互方式登录时，与只是连接以运行单条命令时，shell 的行为会略有不同。.profile 或 .bash_profile 的内容只会为交互式会话执行。如果你没有意识到这个细微差别，你可能会挠头不解：为什么登录并执行命令时一切正常，而只是通过 ssh 登录运行同一条命令时却不行。你可以让交互式和非交互式会话行为一致，从而省去一些麻烦。为此，配置 .bash_profile 引用 .bashrc，并将所有配置放入 .bashrc 中。

下面是一个示例，更好地说明交互式 shell 和非交互式 shell 之间的区别。例如，如果你在 ~/.bash_profile 中为 ll 定义别名，它在交互式会话期间会生效，但在非交互式会话期间将不可用。

### 交互式：

```shell
mac:~ jason $ ssh linuxserver
jason@linuxserver:~$ uptime
11:49:16 up 97 days, 2:59, 5 users, load average:
0.15, 0.25, 0.31

jason@linuxserver:~$ ll
-rw-r--r-- 1 jason jason 221 Nov 13 11:30 file.txt

jason@linuxserver:~$ exit
logout
Connection to 10.0.1.9 closed.
mac:~ jason $
```

### 非交互式：

```shell
mac:~ jason$ ssh linuxserver uptime
11:49:16 up 97 days, 2:59, 5 users, load average:
0.15, 0.25, 0.31
mac:~ jason$ ssh linuxserver ll
bash: ll: command not found
mac:~ jason$
```

```bash
$ cat .bash_profile
# Put our settings in .bashrc so we have the same
# environment for login and non-login shells.
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
```

```bash
$ cat .bashrc
alias ll='ls -l'
HISTFILESIZE=5000
export HISTFILESIZE
```

## 让你的计算机与你交谈

```bash
$ espeak -f file
$ echo text | espeak
```

Espeak 将文本转换为语音。你可以向 espeak 提供一个文件，或通过管道传入文本让它朗读。如果你有一个长时间运行的任务，可以让计算机在任务完成时告诉你，如下例所示。

```bash
$ for VIDEO in $(ls *.mp4 | sed 's/.mp4//')
> do
> avconv -y -quiet -i $VIDEO.mp4 $VIDEO.mp3
> done ; echo "File conversions complete." | espeak
```

## 显示不同时区的当前日期和时间

```bash
$ TZ=<TIMEZONE> date
```

TZ 环境变量指定时区。如果你想知道某个给定时区的时间，可以在 date 命令前加上该环境变量和时区。

```bash
$ TZ=America/Los_Angeles date
Sun Apr  6 19:37:46 PDT 2014
$ TZ=NST date
Sun Apr  6 19:37:48 MST 2014
$ TZ=CST date
Mon Apr  7 02:37:50 CST 2014
$ TZ=UTC date
Mon Apr  7 02:37:53 UTC 2014
```

通常的做法是在服务器上使用 UTC 作为时区。如果你的工作站或笔记本电脑设置为其他时区，你可以创建一个别名，快速获取 UTC 时间。

```bash
$ alias utc='TZ=UTC date'
$ utc
Mon Apr  7 02:35:01 UTC 2014
```

## 在命令行显示日历

```bash
$ cal
$ cal MM YYYY
$ cal YYYY
```

要在命令行显示日历，请使用 cal 命令。使用 -3 选项可显示上个月、当前月和下个月。如果要查看特定月份的日历，请使用 MM YYYY；如果要查看整年的日历，请使用 YYYY。

```text
$ cal
      April 2014
Su Mo Tu We Th Fr Sa
       1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26
27 28 29 30
$ cal -3

      March 2014              April 2014              May 2014
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
                  1  2  3  4  5  6              1  2  3
 2  3  4  5  6  7  8  6  7  8  9 10 11 12  4  5  6  7  8  9 10
 9 10 11 12 13 14 15 13 14 15 16 17 18 19 11 12 13 14 15 16 17
16 17 18 19 20 21 22 20 21 22 23 24 25 26 18 19 20 21 22 23 24
23 24 25 26 27 28 29 27 28 29 30       25 26 27 28 29 30 31
30 31

$ cal 10 2014
       October 2014
Su Mo Tu We Th Fr Sa
          1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30 31
```

## 将 Tar 归档解压到不同目录

```shell
$ tar xf tarfile.tar -C /path/to/directory
```

你可以使用 -C 选项，而不必先切换目录再解压文件。

```shell
$ tar xf projectfiles.tar -C /usr/local/myproject
```

这等价于以下两条命令。

```shell
$ cd /usr/local/myproject
$ tar xf ~/projectfiles.tar
```

## 解压时转换 Tar 文件的目录结构

```shell
$ tar xf tarfile.tar --strip-components=$NUMBER
```

如果你想从某个子目录开始解压 tar 文件，请使用 --strip-components 选项。例如，如果你从 github.com 下载一个发布版本，项目的名称和版本号是 tar 文件中的顶层目录。要解压该目录下的文件，请使用 --strip-components=1。

```shell
$ curl -sLO https://github.com/twbs/bootstrap/archive/v3.1.1.tar.gz
$ tar ztvf v3.1.1.tar.gz | head -1
drwxrwxr-x root/root          0 2014-02-13 12:24 bootstrap-3.1.1
$ tar zxvf v3.1.1.tar.gz --strip-components=1 -C ~/bootstrap-latest
$ ls -l ~/bootstrap-latest
bower.json
CNAME
composer.json
_config.yml
CONTRIBUTING.md
dist
docs
fonts
grunt
Gruntfile.js
js
less
LICENSE
package.json
README.md
test-infra
```

## 在命令行使用电子表格

```shell
$ sc
```

如果你是那种试图在命令行中完成所有事情的人，那么你会喜欢电子表格计算器 SC。另外，如果你熟悉 vi，那么使用 sc 会觉得很自然。除了使用方向键进行导航外，你还可以使用熟悉的 h、j、k 和 l 键。与 vi 一样，g 表示跳转。要跳转到单元格 D4，请输入 gD4。

要输入数字或公式，请导航到要编辑的单元格，并使用 = 后跟数字或公式。要输入左对齐文本，请使用小于号（<）；要输入右对齐文本，请使用大于号（>）。要编辑单元格，请输入 e。要保存文件，请按 P，然后输入文件名。要快速获取帮助，请输入 ?；要退出，请输入 q。要了解更多



如需更多信息，请查看随 sc 附带的教程。

```text
$ sc
A2 (10 2 0) [{sum(A0:A1)}]
             A             B             C
0            1.00
1            3.00
2            4.00
$ sc /usr/share/doc/sc/tutorial.sc
```

## 基础命令行秒表

```text
$ time read
```

按回车后该命令会停止，并显示经过的时间。real 行包含实际经过的时间。

```text
$ time read
real    0m0.047s
user    0m0.000s
sys     0m0.000s
$
```

## 定期重复执行命令并观察其输出变化

```text
$ watch command
```

如果你想监视某个命令的输出，请使用 watch。watch 会定期执行命令并显示其输出。你可以通过向 `-n` 选项提供秒数来控制命令重复的间隔。这是监视进程、磁盘使用情况、登录用户数、队列深度等的绝佳工具。

```shell
$ sudo /usr/local/bin/compress-log-files &
[1] 16560

$ watch df -h /var
Filesystem                     Size  Used Avail Use% Mounted on
/dev/mapper/vg_livecd-lv_root  28G  3.7G  24G  14% /
...

Filesystem                     Size  Used Avail Use% Mounted on
/dev/mapper/vg_livecd-lv_root  28G  3.3G  25G  12% /
/

$ watch -n 1 "ps -ef | grep httpd | grep -v grep | wc -l"
9

...
14

...
29

...
27
$
```

## 在指定时间执行命令

```shell
$ echo "command" | at time
$ at -f file time
```

如果你需要在午夜重启服务器，但又不想熬到那么晚，可以用 at 命令安排。实际上，你可以用 at 安排任何需要在指定时间运行一次的命令或命令集。要列出你的 at 作业，请使用 atq。下面是重启示例。

```text
$ sudo -s
# echo 'reboot' | at midnight
# atq
1    2014-04-13 00:00 a root
# exit
$ exit
```

你可以使用 -f 选项向 at 提供一个包含一系列命令的文件。例如，你可以在周五下午 5:00 给老板发送报告，然后提前离开去打一局高尔夫。如果良心过意不去，你可以用 atrm 删除你的 at 作业。

```text
$ at -f email-tps-report-to-boss 5:00pm friday
job 2 at 2014-04-18 17:00
$ atrm 2
$ atq
$
```

## 与另一位用户共享你的 screen 会话

```text
$ screen -x user/session
```

为了使用 screen 的多用户支持，screen 可执行文件需要设置 setuid root。

```text
sudo chmod u+s /usr/bin/screen
```

必须由一个用户启动 screen 会话。使用 -S 选项为 screen 会话命名会很有帮助。要启用多用户会话，请键入 ctrl-a，然后键入 ":multiuser on<enter>"。要允许某人连接到你的会话，请键入 ctrl-a，然后键入 ":acladd username"。要将另一位用户从 screen 会话中断开，请键入 ctrl-a，然后键入 ":acldel username"。

```text
[jason@linuxsvr ~]$ screen -S for-bob
ctrl-a :multiuser on
Multiuser mode enabled
ctrl-a :acladd bob
```

当另一位用户准备好连接到 screen 会话时，他们输入 screen -x，后跟会话标识符。他们可以通过 PID 或名称连接，即 screen -x 1234 或 screen -x session-name。当他们准备好断开连接时，可以像离开任何其他 screen 会话一样，键入 ctrl-a d 离开。在会话共享期间，双方不仅能看到相同的屏幕，而且都可以通过键入来提供输入。

```text
bob@linuxsvr:~$ screen -ls jason/
There is a screen on:
        5428.for-bob        (Multi, attached)
1 socket in /var/run/screen/S-jason.
bob@linuxsvr:~$ screen -x jason/for-bob
```

```shell
[jason@linuxsvr ~]$
ctrl-a d
[detached]
bob@linuxsvr:~$
```

## 执行别名命令的非别名版本

```shell
$ \aliased-command
```

使用转义字符来忽略命令的别名。例如，如果 "ls" 被别名为 "ls -F"，则使用 "\ls" 执行不带 "-F" 选项的 "ls"。 "-F" 选项会附加文件类型指示符。对于目录，该指示符是正斜杠（/）。

```shell
$ alias ls
alias ls='ls -F'
$ ls
Desktop/  Documents/  Downloads/  examples.desktop
$ \ls
Desktop  Documents  Downloads  examples.desktop
$ ...
```

## 将命令输出保存为图像

```shell
$ command | convert -label @ - image.png
```

要将命令输出捕获到图像文件中，请使用 ImageMagick 软件套件中的 convert 命令。如果你想通过电子邮件将密码发送给某人，但又不想让它在互联网上以纯文本形式传输，可以把它放进图像中。向 label 提供 at 符号（@）时，它会告诉 convert 从 at 符号后面的文件读取输入。短横线表示该“文件”来自标准输入。如果你想创建包含一些文本的简单图像，可以向 label 提供字符串。

## 命令行功夫

```bash
$ echo "bob:changeme" | sudo chpasswd
$ echo "bob:changeme" | convert label:@- password.png
$ convert label:"bob:changeme" same-thing--different-way.png
$ echo "Here's your password. Again." | mail -a passwd.png -s 'Password reset' bob@mycompany.com
$
```

## 关于作者

Jason Cannon 于 1999 年以 Unix 和 Linux 系统工程师的身份开始职业生涯。自那时起，他曾在 Xerox、UPS、Hewlett-Packard 和 Amazon.com 等公司运用自己的 Linux 技能。此外，他还曾为中小型企业担任技术顾问和独立承包商。

Jason 在 CentOS、RedHat Enterprise Linux、SUSE Linux Enterprise Server 和 Ubuntu 方面拥有专业经验。他在个人项目中使用过多种 Linux 发行版，包括 Debian、Slackware、CrunchBang 等。除 Linux 外，Jason 还拥有支持专有 Unix 操作系统的经验，包括 AIX、HP-UX 和 Solaris。

他乐于教别人如何使用并发挥 Linux 操作系统的强大能力，并在 http://www.LinuxTrainingAcademy.com 教授在线视频培训课程。

Jason 还是 *Linux 入门：Linux 操作系统与命令行简介* 的作者。

## 作者的其他书籍

- **LAMP 栈的高可用性**：消除单点故障并提高基于 Linux、Apache、MySQL 和 PHP 的 Web 应用程序的正常运行时间  
  http://www.linuxtrainingacademy.com/ha-lamp-book
- **Linux 入门**：Linux 操作系统和命令行简介  
  http://www.linuxtrainingacademy.com/linux
- **Linux 截图之旅**：最流行的 Linux 发行版图解指南  
  http://www.linuxtrainingacademy.com/screenshots
- **Python 编程入门**：Python 计算机语言与计算机编程简介  
  http://www.linuxtrainingacademy.com/python-book

## 作者开设的课程

- LAMP 栈的高可用性  
  [http://www.linuxtrainingacademy.com/ha-lamp-stack/](http://www.linuxtrainingacademy.com/ha-lamp-stack/)
- Linux 入门  
  [http://www.linuxtrainingacademy.com/lfb-udemy](http://www.linuxtrainingacademy.com/lfb-udemy)
- 5 天学会 Linux  
  [http://www.linuxtrainingacademy.com/linux-in-5-days](http://www.linuxtrainingacademy.com/linux-in-5-days)

## 索引

- **alias**
  - 按日期轻松备份文件，70
  - 在不同时区显示当前日期和时间，89
  - 以表格形式显示输出，14
  - 执行别名命令的非别名版本，98
  - 使用别名修正常见拼写错误，22
- **at**
  - 在指定时间执行命令，95
- **atrm**
  - 在指定时间执行命令，95
- **atq**
  - 在指定时间执行命令，95
- **avconv**
  - 让你的计算机与你对话，89
  - 复用上一条命令中的第 N 个单词，8
- **awk**
  - 命令替换，52
  - 统计字符串出现次数，25
  - 显示两个字符串之间的文本块，19
  - 从文件中提取第 N 行，81
  - 找出你最常使用的命令，11
  - 获取输出行中的最后一个单词，15
  - 每次读取一行输入，54
  - 将命令行输出存储为变量以便稍后使用，53
  - 对文本给定列中的所有数字求和，58




### adduser

- 以 root 身份运行上一条命令，3

### bluefish

- 通过 SSH 将远程服务器上的目录挂载到本地主机，29

### break

- 接受用户输入并将其存储到变量中，56
- 重复执行命令直到成功，62

### cal

- 在命令行显示日历，90

### cat

- 将字符串追加到文件，72
- 统计字符串出现次数，25
- 命令替换，52
- 比较远程文件与本地文件的差异，33
- 在 Windows 格式与 Linux 格式之间转换文本文件，81
- 不使用编辑器从命令行创建文本文件，18
- 删除两个字符串之间的文本块，20
- 清空正在被写入的文件，71
- 获取一行输出中的最后一个单词，15
- 让非交互式 Shell 会话的行为与交互式会话相同，87
- 覆盖文件内容，71
- 从字符串或输出行中删除一个字符或一组字符，24
- 运行不受挂断影响的命令，使作业在你断开连接后继续运行，44
- 保存命令行会话的副本，10
- 对文本指定列中的所有数字求和，58
- 为指定远程主机使用不同的 SSH 密钥，37

### cd

- 切换到上一个工作目录，84
- 将 Tar 归档提取到其他目录，91
- 保存命令行会话的副本，10

### chmod

- 从命令行搜索 Wikipedia，85
- 与其他用户共享你的 Screen 会话，96

### cp

- 命令替换，52
- 快速备份文件，68

### column

- 获取一行输出中的最后一个单词，15
- 以表格格式显示已挂载的文件系统，60
- 以表格形式显示输出，14

### convert

- 将命令输出保存为图像，98

### cut

- 统计字符串出现次数，25
- 从字符串或输出行中删除一个字符或一组字符，24
- 将命令行输出存储为变量以便后续使用，53

### curl

- 从命令行下载网页、HTTP 数据或使用 Web API，46
- 使用 curl 从命令行获取你的公网 IP，30
- 提取 Tar 文件时转换其目录结构，92

### date

- 命令替换，52
- 以不同时区显示当前日期和时间，89

### df

- 一次一行读取输入，54
- 按固定间隔重复执行命令并观察其输出变化，94
- 对输出正文排序，同时保持第一行表头不变，22
- 对文本指定列中的所有数字求和，58

### diff

- 比较远程文件与本地文件的差异，33

### dig

- 从命令行搜索 Wikipedia，85

### dmidecode

- 显示两个字符串之间的文本块，19
- 对文本指定列中的所有数字求和，58

### dos2unix

- 在 Windows 格式与 Linux 格式之间转换文本文件，81

### dpkg

- 从命令行下载网页、HTTP 数据或使用 Web API，46

### du

- 找出谁占用了最多磁盘空间，63
- 重用上一条命令的最后一个单词（最后一个参数），8

### echo

- 接受用户输入并将其存储到变量中，56
- 将字符串追加到文件，72
- 使用 sudo 将文本追加到文件，17
- 更改字符串的大小写，17
- 命令替换，52
- 按日期轻松创建文件备份，70
- 以表格形式显示输出，14
- 以人类可读格式显示你的命令搜索路径，18
- 在指定时间执行命令，95
- 生成随机密码，67
- 让你的计算机对你说话，89
- 一次一行读取输入，54
- 重复执行命令直到成功，62
- 将命令输出保存为图像，98
- 从命令行搜索 Wikipedia，85
- 从命令行发送电子邮件附件，34
- 从命令行发送电子邮件，34
- 将命令行输出存储为变量以便后续使用，53

### espeak

- 让你的计算机对你说话，89

### 事件指示符

- 引用当前命令中的某个单词并重用它，9
- 重复以指定字符串开头的上一条命令，5
- 在替换字符串的同时重复上一条命令，8
- 重用上一条命令的最后一个单词（最后一个参数），8
- 重用上一条命令中的第 N 个单词，8
- 重用上一条命令的第二个单词（第一个参数），7
- 以 root 身份运行上一条命令，3

### exit

- 配置 SSH 根据模式将域名附加到主机名，42
- 断开远程会话并在稍后重新连接，从上次中断处继续，40
- 在指定时间执行命令，95
- 让非交互式 Shell 会话的行为与交互式会话相同，87
- 运行不受挂断影响的命令，使作业在你断开连接后继续运行，44
- 保存命令行会话的副本，10

### file

- 在 Windows 格式与 Linux 格式之间转换文本文件，81

### find

- 易于阅读的递归文件列表，77
- 删除空目录，76
- 找出占用磁盘空间最多的文件，64
- 在多个文件中替换字符串，80

### for

- 命令替换，52
- 将命令行输出存储为变量以便后续使用，53
- 在命令行使用 for 循环，51

### firefox

- 创建 SSH 隧道以访问远程资源，35
- 使用 SSH SOCKS 代理加密你的网页浏览数据，45

### fusermount

- 通过 SSH 将远程服务器上的目录挂载到本地主机，29

### getconf

- 快速判断你使用的是 32 位还是 64 位系统，67

### grep

- 切换到上一个工作目录，84
- 命令替换，52
- 从命令行下载网页、HTTP 数据或使用 Web API，46
- 使用别名修正常见拼写错误，22
- 终止指定用户或程序的所有进程，61
- 覆盖文件内容，71
- 通过管道传给 grep 时保留颜色，16
- 打印包含指定字符串的文件列表，76
- 一次一行读取输入，54
- 按固定间隔重复执行命令并观察其输出变化，94
- 在替换字符串的同时重复上一条命令，8
- 在多个文件中替换字符串，80
- 将命令行输出存储为变量以便后续使用，53
- 去除注释和空行，13
- 使用 less 查看彩色输出，16

### head

- 找出你最常用的命令，11
- 列出按 CPU 使用率排序的进程，66
- 列出按内存使用率排序的进程，65
- 一次一行读取输入，54
- 对输出正文排序，同时保持第一行表头不变，22
- 去除注释和空行，13
- 提取 Tar 文件时转换其目录结构，92

### history

- 清除 Shell 历史记录，12
- 找出你最常用的命令，11

### host

- 重用上一条命令的第二个单词（第一个参数），7
- 从命令行搜索 Wikipedia，85

### hostname

- 配置 SSH 根据模式将域名附加到主机名，42
- 无需密码通过 SSH 登录远程系统，30

### id

- 以 root 身份运行上一条命令，3
- 将命令行输出存储为变量以便后续使用，53

### kill

- 命令替换，52

### killall

- 终止指定用户或程序的所有进程，61

### less

- 通过管道传给 grep 时保留颜色，16
- 使用 less 查看彩色输出，16

### logger

- 在命令行使用 for 循环，51

### ls

- 易于阅读的递归文件列表，77
- 切换到上一个工作目录，84
- 命令替换，52
- 删除空目录，76
- 清空正在被写入的文件，71
- 执行已设置别名的命令的未别名版本，98
- 让非交互式 Shell 会话的行为与交互式会话相同，87
- 快速更改文件扩展名，69
- 快速备份文件，68
- 重复执行命令直到成功，62
- 提取 Tar 文件时转换其目录结构，92

### lsof

- 显示打开的网络连接，32

### mail

- 从命令行发送电子邮件附件，32
- 从命令行发送电子邮件，34



### mkdir
- 删除空目录，76
- 通过 SSH 将远程服务器上的目录挂载到本地主机，29
- 快速备份文件，68
- 将命令输出保存为图像，98

### mount
- 以表格格式显示已挂载的文件系统，60
- 以表格形式显示输出，14

### multitail
- 同时监视多个日志文件，73

### mv
- 快速更改文件扩展名，69
- 引用当前命令中的某个词并复用它，9
- 复用上一条命令中的第 N 个词，8

### mysql
- 创建 SSH 隧道以访问远程资源，35

### ncdu
- 找出谁占用了最多磁盘空间，63

### netstat
- 查明哪些程序正在监听哪些端口，36

### nohup
- 运行不受挂断影响的命令，使作业在你断开连接后继续运行，44

### openssl
- 生成随机密码，67

### passwd
- 将命令行输出存储为变量以便以后使用，53
- 在命令行中使用 for 循环，51

### ping
- 重复执行命令直到成功，62
- 复用上一条命令的第二个词（第一个参数），7

### pkill
- 终止指定用户或程序的所有进程，61

### ps
- 命令替换，52
- 终止指定用户或程序的所有进程，61
- 列出进程，按 CPU 使用率排序，66
- 列出进程，按内存使用量排序，65
- 重复以指定字符串开头的最后一条命令，5
- 对输出正文排序，同时保持第一行表头不变，22

### python
- 通过 Web 界面提供当前目录中的文件，28

### read
- 接受用户输入并将其存储到变量中，56
- 每次读取一行输入，54
- 简易命令行秒表，94

### reboot
- 在指定时间执行命令，95

### reset
- 重置终端模拟器显示，85

### rm
- 复用上一条命令的最后一个词（最后一个参数），8

### sed
- 删除两个字符串之间的文本块，20
- 让你的计算机与你对话，89
- 在多个文件中替换字符串，80

### scp
- 从命令行使用电子表格，93

### screen
- 断开远程会话，稍后重新连接并从上次中断处继续，40
- 与其他用户共享你的 Screen 会话，96

### script
- 保存命令行会话的副本，10

### sort
- 统计字符串出现的次数，25
- 找出你最常用的命令，11
- 找出占用最多磁盘空间的文件，64
- 找出谁占用了最多磁盘空间，63
- 获取一行输出中的最后一个词，15
- 列出进程，按 CPU 使用率排序，66
- 列出进程，按内存使用量排序，65
- 对输出正文排序，同时保持第一行表头不变，22

### ssh
- 通过 SSH 连接时避免输入用户名，39
- 配置 SSH 根据模式为主机名附加域名，42
- 比较远程文件与本地文件的差异，33
- 创建 SSH 隧道以访问远程资源，35
- 断开远程会话，稍后重新连接并从上次中断处继续，40
- 使用 SSH SOCKS 代理加密网页浏览数据，45
- 列出进程，按内存使用量排序，65
- 使非交互式 Shell 会话的行为与交互式会话相同，87
- 运行不受挂断影响的命令，使作业在你断开连接后继续运行，44
- 快速判断你使用的是 32 位还是 64 位系统，67
- 简化多跳 SSH 连接并透明代理 SSH 连接，40
- 无需密码 SSH 登录远程系统，30
- 为指定远程主机使用不同的 SSH 密钥，37

### ssh-copy-id
- 无需密码 SSH 登录远程系统，30

### ssh-keygen
- 无需密码 SSH 登录远程系统，30

### sshfs
- 通过 SSH 将远程服务器上的目录挂载到本地主机，29

### su
- 以 root 身份运行最后一条命令，3

### sudo
- 使用 Sudo 将文本追加到文件，17
- 更改字符串的大小写，17
- 显示两个字符串之间的文本块，19
- 从命令行下载网页、HTTP 数据或使用 Web API，46
- 清空正在被写入的文件，71
- 在指定时间执行命令，95
- 查明哪些程序正在监听哪些端口，36
- 找出占用最多磁盘空间的文件，64
- 找出谁占用了最多磁盘空间，63
- 终止指定用户或组的所有进程，61
- 打印包含指定字符串的文件列表，76
- 快速备份文件，68
- 按固定间隔重复执行命令并观察其变化的输出，94
- 重复以指定字符串开头的最后一条命令，5
- 以 root 身份运行最后一条命令，3
- 保存命令行会话的副本，10
- 将命令输出保存为图像，98
- 通过 Web 界面提供当前目录中的文件，28
- 与其他用户共享你的 Screen 会话，96
- 将命令行输出存储为变量以便以后使用，53
- 在命令行中使用 for 循环，51
- 同时监视多个日志文件，73

### tail
- 更改字符串的大小写，17
- 统计字符串出现的次数，25
- 跟踪文件增长，73
- 在命令行中使用 for 循环，51

### tar
- 将 Tar 归档解压到不同目录，91
- 解压 Tar 文件时转换其目录结构，92

### tee
- 使用 Sudo 将文本追加到文件，17
- 更改字符串的大小写，17

### tree
- 以树形格式查看文件和目录，78

### time
- 简易命令行秒表，94

### tr
- 更改字符串的大小写，17
- 以人类可读格式显示命令搜索路径，18
- 每次读取一行输入，54
- 从字符串或输出行中删除一个字符或一组字符，24

### uname
- 简化多跳 SSH 连接并透明代理 SSH 连接，40

### uniq
- 统计字符串出现的次数，25
- 找出你最常用的命令，11

### userdel
- 以 root 身份运行最后一条命令，3

### vim
- 使用 Vim 通过网络编辑文件，14

### w
- 重复以指定字符串开头的最后一条命令，5

- **wc** — 按固定间隔重复执行命令并观察其变化的输出，94
- **watch** — 按固定间隔重复执行命令并观察其变化的输出，94
- **wget** — 从命令行下载网页、HTTP 数据或使用 Web API，46
- **while**
  - 接受用户输入并将其存储到变量中，56
  - 每次读取一行输入，54
  - 重复执行命令直到成功，62
- **who** — 重复以指定字符串开头的最后一条命令，5
- **whoami**
  - 通过 SSH 连接时避免输入用户名，39
  - 以 root 身份运行最后一条命令，3
- **uptime**
  - 使非交互式 Shell 会话的行为与交互式会话相同，87
  - 以 root 身份运行最后一条命令，3
- **unzip** — 复用上一条命令的最后一个词（最后一个参数），8
- **unix2dos** — 在 Windows 格式与 Linux 格式之间转换文本文件，81
- **yes** — 自动对任何命令回答 Yes，59

## 附录

### 商标

Firefox 是 Mozilla Foundation 的注册商标。

ImageMagick 是 ImageMagick Studio LLC 的注册商标。

Linux® 是 Linus Torvalds 在美国和其他国家的注册商标。

Mac 和 OS X 是 Apple Inc. 的商标，已在美国和其他国家注册。

Open Source 是 Open Source Initiative 的注册认证标志。

Sun 和 Oracle Solaris 是 Oracle Corporation 和/或其关联公司在美国和其他国家的商标或注册商标。

UNIX 是 The Open Group 的注册商标。

Windows 是 Microsoft Corporation 在美国和其他国家的注册商标。

本文提及的所有其他产品名称均为其各自所有者的商标。




## 命令行功夫

![](img/a6ad8334bb72214983f67e3b3c9eb145_131_0.png)

杰森·坎农

http://LinuxTrainingAcademy.com

![](img/a6ad8334bb72214983f67e3b3c9eb145_131_1.png)

