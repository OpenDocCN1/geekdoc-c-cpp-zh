
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

