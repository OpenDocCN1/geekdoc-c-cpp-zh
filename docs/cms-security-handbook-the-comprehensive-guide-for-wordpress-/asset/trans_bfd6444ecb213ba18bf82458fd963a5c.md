

另一种手动备份方法是使用命令行（通过 PuTTY）分别拉取数据库和文件的副本。这种方法的优点是速度快、体积小，但缺点是需要管理多个文件集。先来仔细看看 cPanel 方法。

## 使用 cPanel

在许多托管环境中，商业应用程序 cPanel 都在使用。这是目前最好的网站管理工具之一。它非常稳定且易于学习。

这里列出的步骤假设你的网站主机上安装了 cPanel。本讨论的目的是向你展示如何使用 cPanel 系统进行备份和恢复。

要使用 cPanel，请按照以下步骤操作：

- 1. 在 cPanel 中找到 phpMyAdmin 按钮，点击它打开 phpMyAdmin 管理员界面。

- 2. 找到要导出的数据库。在图 6-1 所示的示例中，所选数据库名为 watcher_cookbook。点击屏幕顶部的 Export 按钮开始该过程。

![](img/8bd670d4939cf71dbd0c6123d1b834ff_218_0.png)

图 6-1：选择数据库

- 3. 在屏幕左侧，点击 Select All 以导出整个数据库。在屏幕右侧，勾选图 6-2 中显示的复选框。

“Add custom comment into header (\n splits lines)”标题下的 Comments 复选框会将日期和时间信息插入到所有表条目中，如下所示。这对于将来恢复时确认正确的数据库很有用。

```sql
-- Table structure for table 'backup_ios_sobi2_categories'

--
-- Creation: Dec 06, 2010 at 05:20 PM
--
-- Last update: Dec 06, 2010 at 05:20 PM
```

你可以用自己喜欢的文本编辑器将其从数据库转储中复制出来。然后，点击 phpMyAdmin 页面中的 SQL 按钮，粘贴数据库转储内容。点击 Go，它应能快速将该表重新插入数据库。

![](img/8bd670d4939cf71dbd0c6123d1b834ff_221_0.png)

图 6-5：完整填充后的数据库

## 使用命令行方法

使用命令行备份数据库是一种高级方法，但这里包含它以确保覆盖全面。

> **注意** 这里描述的步骤用于执行实际备份。如果你决定使用此方法，请务必在你的特定流程中尝试它们。

在此示例中，你与 MySQL 服务器交互，并使用 Linux 内置的工具 tar 进行压缩。接下来的几节将概述你根据所执行任务而要采取的步骤。

### 备份数据库

你可以手动备份数据库，用技术术语来说就是*转储*数据库。你需要 MySQL 用户名和密码。使用 PuTTY 或其他命令行 SSH 工具登录你的服务器。

接下来，使用以下命令登录 MySQL：

```bash
[root@Chapter6-Centos ~]# mysql -u YourUserName -pYourPassword
```

登录服务器后，你可以在井号提示符（#）下使用命令来转储数据库。你需要知道数据库的名称，并且必须为备份文件选择一个名称。

在此示例中，假设你有一个用于 CMS 的数据库，名为 productiondb，并且你想将其转储到 backupdb.sql。以下命令中的 -p 参数指定一个密码。但是，由于命令中没有包含密码，系统会提示你输入密码，如下所示：

```bash
[root@Chapter6-Centos ~]# mysqldump -u root -p productiondb > backupdb.sql
Enter password:
```

如果数据库非常大，你可以使用 tar 命令进行压缩，如下所示：

```bash
[root@Chapter6-Centos ~]# tar cvzf Dec2010.tar.gz backupdb.sql
backupdb.sql
[root@Chapter6-Centos ~]# ls -l
total 208
-rw-r--r-- 1 root root 87287 Dec  8 01:01 backupdb.sql
-rw-r--r-- 1 root root 22983 Dec  8 01:14 Dec2010.tar.gz
```

在第一部分中，你可以看到使用 tar 创建了一个名为 Dec2010.tar.gz 的压缩归档文件。此外，如你所见，体积显著减小，原始文件为 87KB，而归档版本仅为 22KB。根据数据的变化频率，你可能需要每天或每周运行此命令。使用 cron，可以自动执行此任务。

> **注意** 有关设置 cron 作业的简便方法，请参阅 http://dbperf.wordpress.com/2010/06/11/automate-mysql-dumps-using-linux-cron-job/。

### 恢复数据库

当需要恢复数据库（也称为导入）时，请使用以下命令：

```bash
mysql -u root -ppassword database < backupname.sql
```

在此示例中，请注意尖括号（<）指向左侧。这表示导入。指向右侧的尖括号表示导出。以下是该命令以用户名 tom 使用的示例：

```bash
[root@Chapter6-Centos ~]# mysql -u root -ptom productiondb < backupdb.sql
```

> **警告** 此方法非常高级。如果你有任何不安，请不要使用它。你可能导致意外擦除数据。此外，请注意你要写入的文件。如果你不确定内容，可能需要重新创建数据库并导入你的 .sql 文件。

### 压缩文件

转储数据库文件后，你需要压缩存放 CMS 网站的目录。图 6-6 显示了一个基本的 Joomla! 网站。

![](img/8bd670d4939cf71dbd0c6123d1b834ff_223_0.png)

**图 6-6：** Joomla! 网站目录列表

从 pwd（打印工作目录）命令可以看出，该站点的路径是 `/root/CMSWebSite/Joomla`。如果你想压缩整个文件夹，可以使用以下命令：

```bash
tar -cvf Dec-07-2010-backup.tar.gz /root/CMSWebSite/Joomla/*
```

以下响应显示该命令已通过创建文件归档完成了工作：

```text
Dec  8 02:32 Dec-07-2010-backup.tar.gz
```

最常见的错误之一是没有预留足够的空间。如果发生这种情况，只需将目录切换到有空间的文件夹，然后再次运行命令，如下所示：

```bash
cd /root/
tar cvf archivename.tar.gz /path/to/your/site/
```

这会使归档文件位于根文件夹中。在数据库转储和普通 CMS 文件都压缩完成后，你可以选择以下两种方式之一：

- 直接使用 FTP 或 SSH 连接将文件归档和数据库备份归档（或文件）下载下来，并保存在安全的地方。
- 将数据库 `.sql` 文件添加到文件归档中，从而将它们放在一起。

强烈建议你采用第二种方式。务必制作一份副本并离线存储。

你可以将转储的数据库 .sql 文件复制或移动（mv）到与文件备份相同的目录中。复制命令如下：

```text
cp file /path/to/new/location/
```

举个简单的例子，假设你想将 robots.txt 文件复制到 TMP 目录。你可以使用以下命令：

```text
cp robots.txt tmp
```

将数据库备份文件复制到所需位置后，使用以下命令将其添加到归档中：

```text
# tar -rvf Dec-07-2010-backup.tar.gz backupdb.sql
```

rvf 中的 -r 表示追加。

接下来，执行 tar 命令以确保文件完好无损，并且数据库文件已添加：

```text
# tar -tvf Dec-07-2010-backup.tar.gz | more
```

tvf 中的 -t 表示列出。末尾的 more 命令将逐屏显示结果。

这样就完成了数据库和 CMS 文件的捕获与压缩。这对于本书中讨论的所有基于 Linux 运行的 PHP 型 CMS 都适用。Plone 的备份将在本章后面介绍。

### 恢复文件

如果必须恢复，你可以使用前面“使用 cPanel”部分中概述的数据库导入说明进行完整恢复。使用 tar 从归档中恢复文件。你可能需要将它们复制或移动回原位。

以下是可在恢复过程中帮助你的一些命令。要完整解压缩所有文件，请使用以下命令：

```text
# tar -xvzf archive.tar.gz
```

要只提取特定文件，请使用以下命令：

```text
# tar -xvf archive.tar /path/to/file
```

要提取目录，请使用以下命令：

```text
# tar -xvf archive.tar /path/to/dir/
```

