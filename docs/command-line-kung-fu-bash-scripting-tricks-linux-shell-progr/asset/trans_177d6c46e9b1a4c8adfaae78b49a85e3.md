
-   在指定时间执行命令 ........................................ 95
-   与其他用户共享你的屏幕会话 ............................ 96
-   执行某个已设别名的命令的未设别名版本 .................... 98
-   将命令输出保存为图像 ............................... 98
-   关于作者 ........................................................ 100
-   作者的其他图书 .............................................. 101
-   作者的课程 .................................................. 102
-   索引 ................................................................ 103
-   附录 ............................................................... 114
  -   商标 ........................................................... 114

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
