

```text
mysql 4447 94 12.8 2134672 1031064 ?  Sl  10:52
27:39 /usr/libexec/mysqld
$
```

### 快速判断你的系统是 32 位还是 64 位

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

### 生成随机密码

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

