

```
$ mcrypt -d memo1.nc
mcrypt: memo1 already exists; do you wish to overwrite (y or n)?y<Enter>
Enter passphrase: xxxxxxxxx
File memo1.nc was decrypted.
$ more memo1
Dear Jim:
This is to inform you that the second quarter earnings do not
look good. This information will be made public on Monday next
week when The Wall Street Journal reports the company earnings.
Of course, the company stock will take a hit, but we need to keep
the morale of our employees high. I am calling a meeting of the
vice presidents tomorrow morning at 8:00 to talk about this
issue in the main conference room. See you then. Make sure this
information does not get out before time.
Nadeem
$ ls -l memo*
-rw------ 1 sarwar faculty 502 Feb 27 01:42 memo1
-rw------ 1 sarwar faculty 605 Feb 27 01:42 memo1.nc
$
```

你可以使用 -k 选项在命令行中提供密钥，如以下会话所示。

```
$ mcrypt memo1 -k $#!23#$
Warning: It is insecure to specify keywords in the command line
File secret_memo was encrypted.
$ mcrypt -d memo1.nc -k $#!23#$
Warning: It is insecure to specify keywords in the command line
File secret_memo.nc was decrypted.
$
```

你可以使用 mcrypt 的 -z（或 -p）选项在加密前压缩文件。加密后的文件放在 memo1.gz.nc 文件中。解密该文件后，压缩文件会放在 memo1.gz 文件中，需要用 gunzip 解压缩，如以下会话所示。

```
$ mcrypt -k $#!23#$ -z memo1
Warning: It is insecure to specify keywords in the command line
File memo1 was encrypted.
$ ls -l
total 8
-rw------ 1 sarwar faculty 502 Feb 27 09:03 memo1
-rw------ 1 sarwar faculty 445 Feb 27 09:03 memo1.gz.nc
$ mcrypt -k $#!23#$ -d memo1.gz.nc
Warning: It is insecure to specify keywords in the command line
File memo1.gz.nc was decrypted.
$ ls -l
total 12
-rw------ 1 sarwar faculty 502 Feb 27 09:03 memo1
-rw------ 1 sarwar faculty 333 Feb 27 09:03 memo1.gz
-rw------ 1 sarwar faculty 445 Feb 27 09:03 memo1.gz.nc
$ gunzip -v memo1.gz
gzip: memo1 already exists; do you wish to overwrite (y or n)? y<Enter>
memo1.gz:      38.4% -- replaced with memo1
$
```

再次说明，mcrypt 命令不会删除它加密（或解密）的文件，加密后删除原始文件是你的责任。还要注意，即使是超级用户，没有正确的密钥也无法解密加密文件。你可以在加密前后使用 md5sum 命令来验证源文件和解密后的文件是否包含相同的数据。

mcrypt 命令允许你使用它支持的多种加密算法。你可以运行 mcrypt --list-hash 命令来显示这些算法的名称。你可以使用 -h 选项使用这些算法中的任何一种来加密（和解密）文件，如以下会话所示。

```
$ mcrypt --list-hash
Supported Hash Algorithms:
crc32
md5
...
whirlpool
...
md2
$ mcrypt -h whirlpool memo1 -k $#123#$
Warning: It is insecure to specify keywords in the command line
File memo1 was encrypted.
$ ls -l memo1.nc
-rw------- 1 sarwar faculty 658 Feb 27 01:42 memo1.nc
$ mcrypt -d -h whirlpool memo1.nc -k $#123#$
Warning: It is insecure to specify keywords in the command line
mcrypt: memo1 already exists; do you wish to overwrite (y or n)?y<Enter>
File memo1.nc was decrypted.
$
```

如果你的工作需要更高级别的安全文档和通信，你应该使用 openssl 工具。它支持 crypto 库，允许你使用多种加密功能，包括以下内容：

+   - 使用密码进行加密和解密
+   - 创建和管理公钥和私钥
+   - 公钥加密操作
+   - 处理加密电子邮件

openssl 和 crypto 的覆盖范围超出了本书的范围。你可以通过使用 man openssl 和 man crypto 命令了解更多关于它们的信息。

此外，我们在本书网站的第 W26 章第 9.7.3–9.7.5 节中展示了如何使用 Linux gpg 加密工具进行各种磁盘加密形式。gpg 是 Gnu Privacy Guard（GnuPG）的仅 OpenPGP 版本。请参阅 Linux 系统上的 gpg 手册页。

以下章节练习将让你练习使用 mcrypt 命令，并通过动手操作帮助你理解其语义。

## Exercise 7.21

在你的系统上尝试本节中给出的 mcrypt 命令会话。

## Summary

有时需要对文本和非文本文件执行多种高级操作。这些操作包括压缩和解压缩文件内容，对文件排序，在文件系统结构中搜索文件和命令，在文件中搜索特定字符串或模式，执行类似数据库的操作从表中剪切字段或粘贴表，将非 ASCII 文件转换为 ASCII，以及加密和解密文件。Linux 中有多个工具可用于执行这些任务。

其中一些工具能够使用由常量和运算符组成的单个字符字符串来指定一组字符串，称为正则表达式。正则表达式通常被称为搜索模式，用于在文件内容中搜索所需字符串。允许使用正则表达式的实用程序有 awk、ed、egrep、grep、sed 和 vim。在本章中，我们描述了正则表达式及其在 vim、egrep 和 grep 中的使用。

sort 命令可用于对文本文件进行排序。每行包含一个记录，其中包含多个字段，且文件中所有行的字段数相同。文本文件也可以像表一样处理，

使用 cut 和 paste 命令分别允许对表中的列进行剪切和粘贴。sort、cut 和 paste 命令可以通过管道（参见第 9 章）组合起来，根据不同的标准生成表。

find 和 whereis 命令可用于搜索 Linux 文件系统结构以确定文件和命令的位置（绝对路径名）。特别是 find 命令非常强大，允许你根据多种标准（如文件大小）搜索文件。which 命令可用于确定命令执行的是哪个版本，以防系统上存在多个版本。

Linux 还提供了一系列强大的实用程序，用于在文本文件中搜索字符串、表达式和模式。这些实用程序是 grep、egrep 和 fgrep。在这三者中，fgrep 最快但最受限；egrep 是最灵活但最慢的；grep 是中间路线实用程序——速度合理且相当灵活。

gzip 命令可用于压缩和解压缩文件。gunzip 和 gzip -d 命令可用于解压缩 gzip 命令压缩的文件。gzexe 命令可用于压缩可执行文件，gzexe -d 命令可用于解压缩它们。用 gzexe 压缩的文件可以在不显式解压缩的情况下执行。zcat 和 zmore 命令可用于在不显式解压缩的情况下显示压缩文件。bzip2 和 xz 也可用于文件压缩和解压缩。在这三者中（gzip、bzip2 和 xz），xz 在磁盘空间节省、下载时间、网络带宽和解压缩时间方面是最好的。

base64 实用程序在用户想要通过电子邮件发送非 ASCII 文件（如多媒体文件），但邮件系统不允许附件时很有用。base64 实用程序可用于将非 ASCII 文件转换为 ASCII 文件，base64 也可将 ASCII 文件转换回原始非 ASCII 版本。因此，发送者在通过电子邮件发送非 ASCII 文件作为电子邮件正文的一部分之前使用 base64 命令，而接收 uuencoded 文件的接收者使用 base64 将其转换回原始形式。openssl 工具可用于编码和解码数据。

在 Linux 系统中，mcrypt 命令可用于加密和解密用户希望保密的文件。将加密文件转换回原始文件的技术是众所周知的。然而，普通用户并不熟悉这些技术，因此使用 mcrypt 可实现相当好的文件保护方案。它还允许你使用它支持的多种加密算法中的任何一种。

如果你的工作需要更高级别的安全文档和通信，你应该使用 openssl 和 crypto 工具。此外，第 W26 章介绍了使用 gpg 加密工具来实现各种磁盘和文件加密形式。

## Questions and Problems

+   1. 列出你认为的高级文件处理操作中的五个。
+   2. 什么是排序？举例说明你的答案。命名排序的四个应用。命名可用于执行排序的 Linux 实用程序。
+   3. 访问 http://cnn.com/weather 并记录以下亚洲主要城市的最高和最低温度：吉隆坡、卡拉奇、东京、拉合尔、马尼拉、新德里和雅加达。在名为 asiapac.temps 的文件中，构建一个 ASCII 表，每行一个城市，顺序为：城市名称、最高温度和最低温度。以下是一个示例行：
+   
+   Tokyo 78 72
+   
+   给出执行以下操作的命令。
+   a. 按城市名称对表进行排序。
+   b. 按最高温度对表进行排序。
+   c. 按城市名称作为主键、低温度作为次要键对表进行排序。

