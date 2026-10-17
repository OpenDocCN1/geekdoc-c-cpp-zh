
```
# fcontext -a -t public_content_rw_t "/var/ftp/pub/uploads/(.*)*"
# restorecon -R -V /var/ftp/pub/uploads
```

被 SELinux 认为不安全的 FTP 服务器功能具有布尔值（Boolean），允许你启用或禁用这些功能。以下是一些示例：

- 要允许普通用户通过 FTP 服务器进行身份验证并读取和写入文件，布尔值 `ftp_home_dir` 必须开启。这是最常用的 FTP 布尔值之一（默认是关闭的）。若要个人将其开启，请输入：

  ```
  # setbool -P ftp_home_dir on
  ```

- 若要让 SELinux 允许匿名用户向目录读取和写入文件，你需要开启 `allow_ftpd_anon_write` 布尔值：

  ```
  # setbool -P allow_ftpd_anon_write on
  ```

- 若要能够挂载 NFS 或 CIFS (Windows) 共享文件系统并从 vsftpd 服务器共享它们，你需要开启以下两个布尔值：

  ```
  # setbool -P allow_ftpd_nfs_nfs
  ```

  ```
  # setbool -P allow_ftpd_cifs_cifs
  ```

如果你发现无法访问本应可以访问的 FTP 服务器文件或目录，请尝试临时关闭 SELinux：

```
# setforce 0
```

如果你现在可以在 SELinux 的 `Permissive`（允许）模式下访问文件或目录，系统将恢复到 `Enforcing`（强制）模式（`setenforce 1`）。现在，你必须返回 SELinux 设置并找出阻止访问的原因。（更多信息请参阅第 24 章“使用 SELinux 增强 Linux 安全性”。）

# 第四部分：成为 Linux 服务器管理员

## 将 Linux 文件权限与 vsftpd 关联

`vsftpd` 服务器依赖标准的 Linux 文件权限来允许或拒绝访问文件和目录。正如你所预期的，为了让匿名用户查看或下载文件，至少必须为其他用户开启读取权限（`r--`）。要访问目录，至少必须为其他用户开启执行权限（`--x`）。

对于普通用户账户，通用规则是：如果用户可以通过 shell 访问某个文件，那么该用户就可以通过 FTP 服务器访问相同的文件。因此，通常普通用户至少应该能够从他们自己的目录 `get`（下载）和 `put`（上传）文件。在为 FTP 服务器设置好权限和其他安全措施后，你可能还想考虑 FTP 服务器的其他配置设置。

## 配置你的 FTP 服务器

`vsftpd` 服务的大部分配置都在 `/etc/vsftpd/vsftpd.conf` 文件中完成。不同类型服务的示例包含 `/usr/share/doc/vsftpd.conf` 目录中。根据你想要使用 FTP 站点的方式，以下章节讨论了配置 FTP 服务器的几种方法。

记住在进行任何配置更改后要重启 `vsftpd` 服务。

### 设置用户账户

`vsftpd` 服务器自带配置了匿名用户和所有 Linux 用户（即在 `/etc/passwd` 文件中列出的用户）以访问服务器。这是基于以下 `vsftpd.conf` 设置：

```
anonymous_enable=YES
local_enable=YES
```

正如所指出的，尽管设置了 `local_enable`，但 SELinux 实际上阻止了 `vsftpd` 用户登录和传输数据。将 SELinux 切换出 `Enforcing` 模式或设置正确的布尔值可以允许本地账户登录并传输数据。

一些网络公司允许用户使用 FTP 上传其自己的 Web 服务器内容。在某些情况下，用户仅有 FTP 账户，这意味着他们无法登录 shell，但通过创建一个没有默认 shell（实际上是 `/sbin/nologin`）的用户账户，可以防止用户登录 shell，但仍允许 FTP 访问。例如，仅限 FTP 用户账户 `bill` 的 `/etc/passwd` 可能如下所示：

```
bill:x:1000:1000:Bill Jones:/home/bill:/sbin/nologin
```

当用户账户设置 `/sbin/nologin` 为默认 shell 时，任何从控制台或 ssh 以用户 `bill` 登录的尝试都会被拒绝。然而，只要 `bill` 拥有密码并且启用了对 FTP 服务器的本地访问，应该可以通过 FTP 客户端登录 FTP 服务器。

并不是每个在 Linux 系统上拥有账户的用户都能访问 FTP 服务器。`vsftpd.conf` 中的 `userlist_enable=YES` 设置拒绝访问 FTP 服务器。该列表包含了 `/etc/vsftpd/user_list` 文件中列出的所有账户，包括管理员用户 `root`、`bin`、`daemon`、`adm` 等。你可以将你想要拒绝的其他用户添加到此列表中。

如果你将 `userlist_enable` 改为 `NO`，则 `user_list` 文件将变为仅允许访问服务器的用户列表。换句话说，设置 `userlist_enable=NO` 会从 `user_list` 文件中移除所有用户名，添加 `chris`、`joe` 和 `mary` 可能会导致服务器允许这三个用户登录。

无论 `userlist_enable` 的如何设置，`/etc/vsftpd/ftpusers` 文件都包含了被拒绝访问服务器的用户。此外，`ftpusers` 文件包含了管理员用户列表。如果你想拒绝这些访问，可以将更多用户添加到该文件中。

限制系统上的普通账户的一种方法是使用 `chroot` 设置。以下是一些 `chroot` 设置的示例：

```
chroot_local_user=YES
chroot_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
```

# 第 18 章：配置 FTP 服务器

可以从示例文件目录将其复制到 `/etc/vsftpd/vsftpd.conf` 文件中，用于可以在互联网上访问的 FTP 服务器。

## 为互联网环境设置 vsftpd

为了安全地从你的 FTP 服务器向互联网共享文件，你可以通过限制服务器仅允许下载且仅允许匿名用户访问来锁定你的服务器。请先从一个设计用于让 vsftpd 文件在互联网上安全运行的配置开始，备份你的 `/etc/vsftpd/vsftpd.conf` 文件并将其复制覆盖你的 `vsftpd.conf`：

```
/usr/share/doc/vsftpd-/EXAMPLE/INTERNET_SITE/vsftpd.conf
```

接下来的章节描述了 `vsftpd.conf` 的内容。第一部分的设置定义了服务器的访问权限：

### 访问权限

```
anonymous_enable=YES
local_enable=NO
write_enable=NO
anon_upload_enable=NO
anon_mkdir_write_enable=NO
anon_other_write_enable=NO
```

开启 `anonymous_enable` (YES) 并关闭 `local_enable` (NO) 确保了没有人可以使用普通的 Linux 用户账户登录 FTP 服务器。所有人必须通过匿名账户。没有人可以上传文件（`write_enable=NO`）。然后，匿名用户无法上传文件（`anon_upload_enable=NO`）、创建目录（`anon_mkdir_write_enable=NO`）或以其他方式写入服务器（`anon_other_write_enable=NO`）。以下是安全设置：

### 安全

```
anon_read_only=YES
connect_from_port_20=YES
hide_ids=YES
pasv_min_port=50000
pasv_max_port=60000
```

由于 `vsftpd` 守护进程以 `ftp` 用户组的身份读取文件，设置 `anon_read_only=YES` 可确保匿名用户可以看到对其他 (...) 关闭了读取权限的文件，但不能写入文件。`connect_from_port_20=YES` 设置赋予了 `vsftpd` 守护进程微小的权限，通过使用 PORT 风格的数据通信发送客户端可能请求的数据。

使用 `hide_ids=YES` 会隐藏设置在文件上的权限，因此在访问 FTP 站点时，一切看起来都由 `ftp` 用户所有。两个 `pasv` 设置限制了被动模式 FTP（服务器选择一个较高的端口来发送数据）可以使用的端口范围，范围在 50000 到 60000 之间。

### 特性

```
xferlog_enable=YES
ls_recurse_enable=NO
ascii_download_enable=NO
async_stor_enable=YES
```

设置 `xferlog_enable=YES` 后，所有从服务器的传输都会记录在 `/var/log/xferlog` 文件中。设置 `ls_recurse_enable=NO` 可以防止用户在大站点上递归列出 FTP 目录类型（换句话说就是 -R 命令），这可能会耗尽磁盘资源。禁用 ASCII 会强制所有下载使用二进制模式（防止文件被转换为 ASCII，这对于二进制文件是不恰当的）。`async_stor_enable=YES` 确保了某些 FTP 客户端在中止传输时不会挂起。

### 性能

```
one_process_model=YES
idle_session_timeout=120
data_connection_timeout=300
accept_timeout=60
connect_timeout=60
anon_max_rate=50000
```

设置 `one_process_model=YES` 后，性能可以提高，因为 `vsftpd` 为每个连接启动一个进程。将 `idle_session_timeout` 从默认的 300 秒减少到 120 秒，会导致空闲的 FTP 客户端被断开。`accept_timeout` 设置为 60 秒允许 PASV 连接被接受。`connect_timeout` 设置了远程客户端响应的时间，以建立 PORT 风格的数据连接。`anon_max_rate` 设置为 50000 可以通过限制每个客户端消耗的带宽来提高服务器的性能。

## 使用 FTP 客户端连接你的服务器

许多 Linux 程序可以用来连接到 FTP 服务器。如果你只是想从你的 FTP 服务器下载一些文件，Firefox 浏览器提供了一个简单的界面。对于客户端与服务器之间更复杂的交互，可以使用命令行 FTP 客户端。接下来的章节描述了这些工具。

### 从 Firefox 访问 FTP 服务器

Firefox 浏览器提供了一种快速方便的方法来测试你的 FTP 服务器或访问任何公共 FTP 服务器。在你自己的系统中，在位置框输入 `ftp://localhost`。如果你的服务器是可以访问的，你应该看到类似于图 18.2 所示的内容。

图 18.2

![](img/3886a4c1a684ab63e25e82e0a2d63de9_532_0.png)

要在 Firefox 中以特定用户登录 FTP 服务器，可以在主机名前之前加上 `username:password@`。例如：

```
ftp://chris:MypassWds@localhost
```

如果用户名密码正确，你应该立即看到主目录的内容。点击文件夹打开。点击文件下载或查看。

### 使用 lftp 命令访问 FTP 服务器

要从命令行测试你的 FTP 服务器，可以使用 `lftp` 命令。要在 Fedora 或 RHEL 中安装 `lftp` 命令，请在命令行输入以下命令：

```
# yum install lftp
```

如果你只使用 `lftp` 命令配合你尝试访问的 FTP 服务器名称，该命令将尝试以匿名用户的身份连接 FTP 服务器。通过添加 `-u username`，你可以在提示时输入用户密码，并以登录用户的身份访问 FTP 服务器。

在你添加了用户和密码信息后，你会得到一个 `lftp` 提示符，可以开始输入命令。当连接到服务器建立时...

图 18.3
