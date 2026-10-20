

## 基本文件处理

与 head 命令一样，如果没有给出文件列表作为参数，tail 命令会从标准输入读取输入。下面的会话演示了 tail 命令在带选项和不带选项情况下的用法。我们使用与 head 命令相同的示例文件。`tail sample` 命令显示示例文件的最后十行（tail 的默认行数），`tail -5 sample` 命令显示示例文件的最后五行。`tail +12 sample` 命令显示从第 12 行开始的文件尾部内容（而不是最后 12 行）。最后，`tail -5r sample` 命令以相反顺序显示示例文件的最后五行。

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

下面的命令显示 otto 和 data 文件具有正确的 PostScript 和 uuencode 编码的尾部内容。

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

当你需要查看正在增长的文件的尾部内容时，`tail` 命令的 **-f** 选项非常有用。当你运行一个需要很长时间（几分钟、几小时或几天）才能完成的模拟程序，并且希望在该程序生成数据时查看这些数据时，这种情况经常出现。如果你的 Linux 系统运行 X Window 系统（参见第 W28 章），这样做会很方便。在 X 环境中，你可以在 *xterm*（控制台窗口）中运行 `tail` 命令，在新数据生成时对其进行监控，同时继续做其他工作。下面的命令显示 **sim.data** 文件的最后十行，并在有新行追加到该文件时显示这些新行。你可以按 `<Ctrl+C>` 来终止该命令。

```
$ tail -f sim.data
... last 10 lines of sim.data ...
... more data as it is appended to sim.data ...
```

有时，在排查 Linux 系统问题时，系统管理员需要显示 **/var** 目录中不断增长的文件，因为内核和应用程序不断向其中追加新消息，包括 **/var/spool**、**/var/mail** 和 **/var/log** 目录中的文件。

传统上，系统管理员可以使用 `tail -f` 命令查看这些文件被追加的内容，如下面的会话所示，该命令显示 **/var/log/messages** 文件的最后十行，并在内核和应用程序向该文件追加新消息时继续显示它们。

```
$ tail -f /var/log/messages
... last 10 lines of /var/log/messages ...
... more data as it is appended to /var/log/messages ...
```

借助 Linux 所有主要分支均可使用的 systemd，系统管理员还可以使用 `journalctl -f` 命令实时显示正在写入系统日志的消息。使用 `journalctl -r` 命令可以查看写入系统日志的最后几行或最新几行。我们将在第 18 章以及本书网站上关于 systemd 的第 W27 章中展示 journalctl 的更多用途。

在下面的本章练习中，要求你使用 cat、head、more、pr 和 tail 命令显示文本文件的不同部分，分别带和不带页面标题和编号。

### 练习 6.3

将第 6.2.1 节中使用的 **student_records** 文件放入当前目录。再向其中添加十条学生记录。使用 `cat student_records` 和 `cat -n student_records` 命令显示该文件的内容。这两个命令的输出有什么区别？

### 练习 6.4

使用 `more` 和 `pr` 命令显示 **student_records** 文件。你使用了哪些命令行？

### 练习 6.5

显示 **/etc/passwd** 文件中位于包含你的登录名的那一行之前的两行。你使用了哪条命令行？

### 练习 6.6

给出显示 **student_records** 文件前七行和后七行的命令。

### 6.3 复制、移动和删除文件

在本节中，我们介绍在文件结构中对文件执行复制以及移动/重命名和移除/删除操作的命令。我们将讨论的命令是 `cp`、`mv` 和 `rm`。

#### 6.3.1 复制文件

Linux 中用于复制文件的命令是 cp。下面是该命令的简要说明。

**语法：**`cp [options] file1 file2`

**用途：**将 file1 复制到 file2。如果 file2 是一个目录，则在此目录中创建 file1 的副本。

**常用选项/特性：**

-   `-f` 如果对 file2 没有写权限，则强制复制
-   `-i` 如果 file2 已存在，在覆盖前提示
-   `-p` 保留文件属性，如所有者 ID、组 ID、权限和修改时间
-   `-r` 递归复制文件和子目录

你必须拥有读取源文件（file1）的权限，以及执行（搜索）包含 file1 和 file2 的目录的权限。此外，如果 file2 尚不存在，你必须拥有包含 file2 的目录的写权限。如果 file2 已存在，你不需要对包含它的目录拥有写权限，但必须对 file2 拥有写权限。如果目标文件（file2）已存在，默认情况下，只要你对该文件拥有写权限，它就会被覆盖，而不会通知你。要在覆盖已存在的文件之前得到提示，你需要使用 -i 选项。如果你没有目标文件的写权限，系统会通知你这一点。如果你没有源文件的读权限，屏幕上将出现错误消息。

下面的 cp 命令行将 temp 复制到 temp.bak。ls 命令显示执行 cp 命令前后当前目录的状态。图 6.1 以图形形式显示了相同的信息。

```
$ ls
memo  sample  temp
$ cp temp temp.bak
$ ls
memo  sample  temp  temp.bak
$
```

如果 temp 不存在，或者它存在但你没有权限读取其内容，该命令将返回错误消息。如果 temp.bak 已存在且你没有写权限，该命令也会返回错误消息。下面的会话说明了这些情况。第一个错误消息是因为当前目录中不存在 letter 文件而被报告的。第二个错误消息是因为你没有读取 sample 文件的权限而被报告的。最后一个命令报告错误消息，是因为 temp.bak 已存在且你没有对其的写权限。你可以使用 -f 选项来克服写权限的缺失并强制复制，如下一条命令所示。ls -l memo temp.bak 命令用于表明复制确实已经发生；也就是说，

![](img/2a18e06cd9c6395e451f26126ecba1fd_157_0.png)

图 6.1 temp 文件被复制到 temp.bak 前后当前目录的状态。

数据已被复制，但该文件的时间戳是当前时间。如果你想同时复制源文件的数据和属性，需要使用带 -f 和 -p 选项的 cp 命令，如下面的最后一条 cp 命令所示。最后一条 ls -l memo temp.bak 命令用于表明数据和文件属性（如时间戳）都已复制。

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

下面的命令在你的主目录中复制 .profile 文件，并将其放到同样位于你的主目录中的 sys.backups 子目录下的 .profile.bak 文件中。由于路径名以你的主目录开头，因此无论你运行该命令时位于哪个目录，该命令都能正常工作。你应该在更改 ~/.profile 文件中指定的运行时环境之前执行此命令，以便在设置新环境时出现问题的情况下，拥有先前工作环境的备份副本。如果 ~/.profile 不存在、你没有读取它的权限、~/sys.backups 目录不存在或你没有对其的执行（搜索）和写权限，或者 .profile.bak 已存在但你没有对其的写权限，该命令都会产生错误消息。

```
$ cp ~/.profile ~/sys.backups/.profile.bak
$
```

下面的命令将当前目录中所有以字符串 lab 开头的文件复制到目录 ~/courses/ee446/backups 中。如果 backups 目录中已经存在任何源文件，该命令还会提示你是否覆盖。在这种情况下（即正在复制多个文件时），如果 backups 不是目录或不存在，屏幕上会显示错误消息，通知你目标必须是一个目录。

```
$ cp -i lab* ~/courses/ee446/backups
$
```

如果你要把整个目录复制到另一个目录，需要使用带 -r 选项的 cp 命令。该选项会递归地将文件和子目录从源目录复制到目标目录。这是一个有用的选项，你可以用它定期创建重要目录的备份。因此，下面的命令将 ~/courses 目录递归复制到 ~/backups 目录。

```
$ cp -r ~/courses ~/backups
$
```

