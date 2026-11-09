

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

