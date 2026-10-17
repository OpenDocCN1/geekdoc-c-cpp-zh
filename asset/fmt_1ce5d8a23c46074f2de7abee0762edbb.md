
`user='guest'` `host='hp720.sas.com'`

`recfm=v` `prompt;`

```
data mydata / view=mydata; /* 创建视图 */
infile myfile;
input X 10. y 4.;
run;
```

```
proc print data=mydata; /* 打印数据 */
run;
```

### 示例 3：在远程主机上创建文件

此示例在主机 `winnt.pc` 上为用户 `bbailey` 在 `c:\remote` 目录下创建一个名为 `test.dat` 的文件。

```sas
filename create 'c:\remote\test.dat'
host='winnt.pc'
user='bbailey'
data_null;
do i=1 to 10;
put i=
end;
run;
```

### 示例 4：在 z/OS 上读取 S370V 格式文件

此示例从 `zos` 系统读取 `s370v` 格式文件。有关 `RCMD=` 选项的更多信息请参见第 121 页。

```sas
filename viewdata ftp 'sluggo.data'
user='sluggo' host='zoshost'
s370v rcmd='site rdw'
data mydata;
infile viewdata;
input
run;
```

### 示例 5：匿名登录 FTP

此示例显示了如何匿名登录（如果主机接受匿名登录）。

注意：某些匿名 FTP 服务器需要密码。如果需要，通常使用你的电子邮件地址。参见第 120 页的“FTP 选项”。

```sas
filename anon ftp 'ls host=130.96.6.1'
user='anonymous';
data_null;
infile anon;
input;
list;
run;
```

### 示例 6：使用编码密码

此示例显示如何在 `FILENAME` 语句中使用编码密码。

在另一个 SAS 会话中，使用 `PWCODE` 过程对密码进行编码并记录输出。

```sas
proc pwencode in="MyPass1";
run;
```

SAS 日志中会出现以下输出：

```sas
(sas001) TX1QXZnM2==
```

你现在可以在批处理中使用整个编码密码字符串。

```sas
filename myfile ftp 'sales' cd=/u/kudzu/mydata'
user='tjbarry' host='hp720.hp.mycompany.com'
pass="sas001 TX1QXZnM2="
```

### 示例 7：导入数据集

此示例使用 `CIPORT` 过程从命名主机导入传输数据集。新数据集将位于本地 `SASUSER` 库中。注意，用户名和密码可以是 SAS 宏。如果你指定了完全限定的数据名，请使用双引号和单引号。否则，系统将向你指定的名称添加前缀。

```sas
#let user=calvin
#let pw=XXXX;
filename inp ftp "calvin.mat1.cpo" user="&user"
```

# 126 第2章 · SAS 语句字典

```sas
pass="&&pw" rcmd='binary'
host='mvhost1'
nproc copy library=sasuser infile=inp
nrun;
```

### 示例 8：传输 SAS 库

此示例使用 `CPORT` 过程将 SAS 库传输到名为 `mvhost1` 的主机，供用户 `calvin` 使用。将在主机上创建一个名为 `userid.mat64.cpo` 的新顺序文件，其 `recfm` 为 `fb`，`lrecl` 为 80，`blocksize` 为 8000。

```sas
filename inp ftp="mat64.cpo" user=calvin
pass="xxxx" host='mvhost1'
lrecl=80 recfm=f blocksize=8000
rcmd='site blocksize=800 recfm=fb lrecl=80;
proc copy library=mylib infile=inp;
run;
```

### 示例 9：使用 XPORT 引擎创建传输库

此示例在主机 `mvhost1` 上创建一个新的 SAS 库。`FILENAME` 语句将文件指针分配给新数据集。注意使用 `RCMD` 选项来指定重要的文件属性。`LIBNAME` 语句使用与文件指针相同的库并将其分配给 `XPORT` 引擎。`PROC COPY` 步骤将 SAS 库中被 `MYLIB` 引用的所有数据集复制到 `XPORT` 引擎。`PROC CONTENTS` 步骤的输出确认查询成功：

```sas
filename inp ftp="mat65.cpo" user=calvin
pass="xxxx" host='mvhost1'
lrecl=80 recfm=f blocksize=8000
rcmd='site blocksize=8000 recfm=fb lrecl=80';
libname mylib 'SAS-library';
filename inp export;
proc copy in=mylib out=inp data;
run;
proc contents data=inp_all_;
run;
```

> 注意：有关 XPORT 引擎的更多信息，请参阅《SAS 语言参考》第 35 章中的“传输引擎”，以及《移动和访问 SAS 文件》第 4 章中的“概念”和“XPORT 引擎局限性”。

### 示例 10：从目录读取和写入

此示例从 UNIX 主机上的目录读取文件 `ftpmeml`，并将文件 `ftppout1` 写入另一个 UNIX 主机的不同目录。

```sas
filename indir ftp '/user/proj2/dir/' DIR
host='host1.mycompany.com'
user="xxxx"; prompt;
filename outdir ftp '/user/proj2/dir' DIR FILEEXT
host='host2.mycompany.com'
user="xxxx"; prompt;
data_null;
inindir (ftpmeml) truncate;
input;
file outdir(ftpout1);
put infile_;
run;
```

# FILENAME 语句，FTP 访问方法 127

`ftppout1` 被写入到 `/user/proj2/ftpout1.DATA`。注意，`ftppout1` 文件附加了 `DATA` 类型的成员，因为在输出文件的 `FILENAME` 语句中指定了 `FILEext`。更多信息请参阅第 119 页的 `FILEext`。

注意：`ODS` 目标不需要 `DIR` 选项。

以下示例写入一个输出文件并将其传输到 `ODS` 指定的目标。不需要 `DIR` 选项。

```sas
filename output ftp="user/ftdir/" host="host.fyi.company.com" user="userid"
pass="userpass" recfm=debug;\ods html body=body.html path=output;
proc print data=sashelp.class;run;
```

要将多个文件导出到远程目录，必须在 `FILENAME` 语句中指定 `DIR` 选项。因此，在使用 `ODS HTML` 目标创建外部图形文件时，需要两个 `FILENAME` 语句：一个用于 HTML 文件，另一个用于图形文件。以下示例说明了需要两个 `FILENAME` 语句的情况。

```sas
filename output1 ftp="filetext" host="host.unx.company.com"
user="userid" pass="userpass" recfm=debug;
filename output2 ftp="user/dir" filetext host="host.unx.company.com"
user="userid" pass="userpass" recfm=debug;\ods html body=body.html path=output2
frame="frames.html" contents="contents.html";
proc gstit;
run;
guit;
```

### 示例 11：使用代理服务器

此示例在 FTP 访问方法使用了代理服务器。用户 ID 和密码通过代理服务器发送。

```sas
test ftp 'ls'
host="proxy.server.xxx.com"
user="userid@ftpservername"
pass="xxxxxx"
cd="pubdir/"
data=null;
infile test truncate;
input $256;
put a=;
run;
```

# 另另

语句：

- 第 93 页的“`FILENAME Statement`”
* 第 100 页的“`FILENAME Statement, CATALOG Access Method`”
* 第 105 页的“`FILENAME Statement, EMAIL (SMTP) Access Method`”
* 第 133 页的“`FILENAME Statement, SOCKET Access Method`”
* 第 128 页的“`FILENAME Statement, SFTP Access Method`”

## FILENAME 语句，SFTP 访问方法

允许您使用 `SFTP` 协议访问远程文件。

#### 有效区域： | 任意 |
| :--- | :--- |
| 类别： | 数据访问 |

## 语法

```sas
filename fileref 'external-file' <sftp-options>;
```

## 参数

`fileref` 是有效名称。

> 注意：有关 XPORT 引擎的更多信息，请参阅《SAS 语言参考》第 35 章中的“传输引擎”，以及《移动和访问 SAS 文件》第 4 章中的“概念”和“XPORT 引擎局限性”。

### DIR

允许您访问目录文件。指定为主机的目录名称。

## 提示：

- 如果您希望 SFTP 创建目录，则结合 `DIR` 选项使用 `NEW` 选项。如果目录已存在，`NEW` 选项将被忽略。

如果省略 `NEW` 选项并指定了无效目录，则不会创建新目录，您将收到错误消息。

# 130 第 2 章 • SAS 语句字典

要显示不带前导点的文件（例如 `.Authority`），请使用 `LS` 选项。

**提示：** 若要返回文件子集的列表，除 `LSA` 外，请使用 `LSFILE` 选项。

# LSFILE='字符字符串'

与 `LS` 选项结合使用，指定一个字符字符串，允许你请求从工作目录获取文件子集的列表。请将字符字符串括在引号中。

**限制：** 只有在指定了 `LS` 或 `LSA` 的情况下才能使用 `LSFILE`。

**提示：** 你可以在 `'字符字符串'` 中包含通配符。

**示例：** 此语句列出所有以 `sales` 开头并以 `sas` 结尾的文件：
```bash
filename myfile sftp '' lsfile='sales.sas' other-sftp-options;
```

# MGET

传输多个文件，类似于 SFTP 的 `MGET`。

**提示：** 整个文件将作为一个文件进行传输。但是，每当开始传输每个新文件时，`EOV=` 变量会被设置为 1。

# NEW

指定在你使用 `DIR` 选项时，让 SFTP 创建目录。

**限制：** z/OS 下不可用 `NEW` 选项。

**提示：** 如果目录已存在，则将忽略 `NEW` 选项。

# OPTIONS=

指定 SFTP 配置选项，例如端口号。

# PATH

指定 SFTP 可执行文件的位置，如果它未安装在 `PATH` 或 `$PATH` 搜索路径中。

**提示：** 建议将 OpenSSH `'SFTP'` 可执行文件或 PUTTY 的 `'PSFTP'` 可执行文件安装在可以通过 `PATH` 或 `SPARSE` 路径访问的目录中。

# RECF=recfm

其中 `recfm` 是两种记录格式之一：

-   - `F`
固定记录格式。因此，所有记录的大小均为 `LRECL`，且没有行分隔符。

-   - `V`
是变长记录格式（默认值）。在此格式下，记录长度不一，并用换行符分隔。数据以镜像（二进制）模式传输。

默认值：`V`

# USER='用户名'

指定用户名。

**要求：** Windows 上的 `PUTTY` 客户端需要用户名。

**提示：**

-   在 fact公钥认证时，`LINUX` 或 `UNIX` 主机通常不需要用户名。

-   使用 SSH 代理进行公钥认证是连接到远程 `SSHD` 服务器的推荐方法。

# FILENAME 语句，SFTP 访问方法 131

`WAIT_MILLISECONDS=`毫秒
指定 SFTP 的毫秒响应时间。

默认值：1,500 毫秒
提示：如果你在日志中收到超时消息，请使用 `WAIT_MILLISECONDS` 选项增加响应时间。

## 详情

## 基础

安全文件传输协议 (`SFTP`) 为跨网络在两个主机（客户端和服务器）提供安全连接和文件传输。命令和数据都经过了加密。客户端与远程主机（OpenSSH SSH 服务器）建立连接。

使用 `SFTP` 访问方法，你可以从网络上运行着 OpenSSH SSHD 服务器的任何主机读取或写入数据。客户端和服务器应用程序可以位于同一台计算机上，也可以位于网络连接的不同计算机上。

具体的实现细节取决于 OpenSSH SSHD 服务器的版本以及该站点的配置。

`SFTP` 访问方法依赖于针对 OpenSSH 命令的默认发送和回复消息。修改这些消息的自定义 OpenSSH 安装将禁用 `SFTP` 访问方法。

你必须安装相应的客户端软件才能使用 `SFTP` 访问方法。`SFTP` 访问方法仅支持以下 SSH 客户端。

+   - OpenSSH – UNIX
-   PUTTTY – Windows

> 注意：`SFTP` 访问方法不支持密码验证。
注意：使用 SSH 代理进行公钥认证是连接到远程 SSH 服务器的推荐方法。

> 注意：如果你在运行 `SFTP` 访问方法时遇到困难，请尝试在不涉及 SAS 系统的情况下，手动验证 SFTP 客户端对 OpenSSH SSHD 服务器的访问。在不涉及 SAS 系统的情况下手动验证 SFTP 访问将确保你的 SSH/SSHD 配置和密钥认证设置正确。

# SFTP 访问方法和 SFTP 提示符

`SFTP` 访问方法仅支持以下提示符。更改提示符将禁用 `SFTP` 访问方法。

+   - 对于 OpenSSH：
`sftp >`
`sftp >`
-   对于 PUTTTY：
`psftp >`

## 比较

与 `SFTP get` 和 `put` 命令一样，`SFTP` 访问方法允许你下载和上传文件。然而，该方法直接将文件读取到你的 SAS 会话中，而无需先将其存储在你的系统中。

## 示例

示例 1：连接到标准端口上的 SSHD 服务器

此示例在连接到标准端口上的 SSHD 服务器后，使用 SFTP 访问方法读取名为 `test.dat` 的文件：

```sas
filename myfile sftp '/users/xxxx/test.dat' host="unixhost1"
data_null;infile myfile truncate;
input a $25;
run;
```

示例 2：连接到非标准端口上的 SSHD 服务器

此示例在连接到端口 4117 上的 SSHD 服务器后，使用 SFTP 访问方法读取名为 `test.dat` 的文件：

```sas
filename myfile sftp '/users/xxxx/test.dat' host="unixhost1" options="-oPort=4117"
data_null;\infile myfile truncate;
input a $25;
run;
```

示例 3：将 Windows PUTTY 客户端连接到 SSHD 服务器

此示例在连接到 SSHD 服务器后，使用 SFTP 访问方法写入名为 `test.dat` 的文件：

```sas
filename myfile sftp '/users/xxxx/test.dat' host="unixhost1"
data_null;infile myfile truncate;
input a $25;
run;
```

示例 4：从目录中读取文件

此示例在连接到标准端口上的 SSHD 服务器后，使用 SFTP 访问方法从目录读取 `test.dat` 和 `test2.dat`：

```sas
filename myfile sftp '/users/xxxx/' host="unixhost1"
data_null;infile myfile truncate;
input a $25;
infile test.dat; truncate;
input b $25;
run;
```

示例 5：使用批处理文件

在此示例中，当处理 `INFILE` 语句时，使用 SFTP 关联的批处理文件：

```sas
filename process sftp 'sftcdda' host="unixhost1"
data_null;infile process;
run;
```
