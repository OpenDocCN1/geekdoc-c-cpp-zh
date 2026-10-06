
从 MySQL 5 版本开始，引入了 `information_schema` 数据库。这个数据库是一个元数据库，包含了 MySQL 数据库中所有元素的信息。我们可以查询 `information_schema` 来查找我们有权访问数据库的任何信息。我们已经见过了要利用的应用程序代码，但假设我们没见过，我们就不知道登录表的名称。通过使用 `information_schema` 数据库，我们可以找到这些信息。

我们正在利用的查询看起来如下：
`select from wordlist where word like '%${POST['word']}'`

我们真正需要做的是将这个查询修改为能够显示来自 `information_schema` 数据库信息的查询。数据库中有一个表，包含了关于我们可以访问的所有表的信息。这个表被称为 `TABLES`，它包含了关于我们可以访问的数据库和表的所有元数据，包括表所在的数据库以及表本身的名称。我们将构建一个查询来强制 `select` 语句返回这些信息。其中，我们的输出只打印了返回数据的第一个元素。我们需要两个部分且只有一个字段来存放它们，因此我们必须进行一些额外的“魔法操作”，将字段中的数据合并为一个，以便正确输出。

我们并不太关心 `wordlist` 表中的数据，因此我们修改查询，使其不返回任何此类信息，只返回我们想要的信息。我们对单词 `qqqq` 进行普通搜索。它没有返回结果，因此这是确保不返回任何 `wordlist` 数据的一种好方法。我们将使用 `UNION` 语句将两个查询合并，并同时返回它们的输出。在执行 SQL 注入（SQLi）时，`UNION` 关键字非常重要，因为它允许我们从通常在查询中无法访问的表中返回额外信息。让我们使用 `UNION` 语句开始从 `information_schema` 数据库获取信息。

我们发布查询：
`qqqq' union select TABLE_NAME from information_schema.TABLES --`

我们看到了所有我们可以访问的表的输出。问题是，其中许多表本身就是 `information_schema` 数据库的表。我们并不在乎这些，所以扩展我们的查询，使其只返回不在 `information_schema` 数据库中的表名。

```
qqqq union select TABLE_NAME from information_schema.TABLES WHERE TABLE_SCHEMA != 'information_schema' -
```

现在，我们只看到感兴趣的表。

然而，除了表名之外，知道数据库名称通常也很方便，但我们修改了查询，以便在一个字段中同时看到两者。为了将多个部分的信息合并到一个字段中，我们可以使用 MySQL 的 `CONCAT` 指令，将所有信息连接成单个字符串。我们再次修改查询。

```
qqqq union select CONCAT(TABLE_SCHEMA,'|',TABLE_NAME) from information_schema.TABLES WHERE TABLE_SCHEMA != 'information_schema'
```

现在，我们的查询使用管道符作为分隔符，将数据库名称（或模式名称）与表名拼接。这应该会给我们类似于图 10.8 的输出，显示我们创建的两个表。

![](img/42f332b2adf7dab7e681e5d6cdd2074c_399_0.png)

搜索：[搜索!]

搜索结果：
login|varchar
pass|varchar

# 图 10.8 查看 login 和 pass 字段

通过 SQLi。

我们看到输出包含两个表：`testapp` 数据库的 `login` 表和 `wordlist` 表。我们现在知道想要导出哪个表了，但不知道字段是什么。`information_schema` 数据库也会帮助我们解决这个问题。数据库中还有另一个表，包含了每个数据库所有列的信息，即 `COLUMNS` 表。我们可以查询 `COLUMNS` 表的 `COLUMN_NAME` 和 `DATA_TYPE` 字段，查看每个字段的名称以及它包含的数据类型。让我们修改最后一次查询，获取这些信息。`qqqq' union select CONCAT(COLUMN_NAME,'|',DATA_TYPE) from information_schema.COLUMNS WHERE TABLE_NAME = 'login--`

我们应该能够返回表中每个变量的名称以及与其关联的数据类型。将其限制在 `login` 表，这样我们就不担心额外的数据。一旦执行查询，我们就返回了每个变量及其包含的数据类型。图 10.8 显示有两个字段：`login` 字段和 `pass` 字段。它们包含 `varchar` 数据，这是一种字符串数据类型。我们现在有了从 `login` 表中获取登录名和密码的所有信息。

我们再次构建了一个新查询；这次我们确切知道想要什么。我们需要 `login` 表的 `login` 和 `pass` 字段。我们创建查询字符串。

```
qqqq' union select CONCAT(login,'|',pass) from login
```

我们从表中选择 `login` 和 `pass` 字段并用管道符将它们连接起来，将两个字段作为一个字符串返回。图 10.9 显示我们之前创建的默认登录已导出到屏幕上。我们可以看到登录是 `admin`，密码是 `admin123`。当我们回到搜索页面尝试这些凭据时，我们只需证明它们是有效的。我们现在成功地利用 SQLi 漏洞不仅访问了应用程序，还检索了通常无法访问的数据。

![](img/42f332b2adf7dab7e681e5d6cdd2074c_401_0.png)

搜索：[ ] 搜索!

搜索结果：
admin|admin123

# 图 10.9 使用 SQLi 获取用户名和密码。

# Microsoft SQL Server 上的 SQLi

在 MySQL 和 Microsoft SQL Server 上执行 SQLi 的步骤非常相似。我们正在利用代码中类似的问题；由于 SQL 是一种标准，语言本身的映射非常接近。Microsoft SQL Server 包含一个如果我们不包含在本章中将是疏忽的功能：一个名为 `xp_cmdshell` 的方便存储过程，它允许 SQL 服务器执行 shell 命令。此存储过程通常是关闭的，但如果我们发现某个服务器管理员正在运行数据库管理员的程序，我们可以自己将其开启。存储过程是运行在 SQL 服务器内部的代码段，并构建在函数中，我们只需通过向它们传递参数即可执行它们，当我们在有此类需求时就不需要重复代码。在本节中，我们将查看带有登录页面的理论应用程序。我们将首先验证该功能是否启用，尝试启用该功能，最后使用 `xp_cmdshell` 函数在服务器上执行命令。

# 验证漏洞

首先需要通过页面验证漏洞。当我们第一次到达页面时，看到了登录屏幕。当我们在页面中输入随机内容时，我们看到登录失败，但当我们在登录字段中输入字符串 `' or l=1 --` 时，我们获得了应用程序的访问权限。我们需要确保在 Microsoft SQL Server 中两个横杠后面包含空格，以确保注释被正确解释。该应用程序的下一步是检查 `xp_cmdshell` 是否启用。但是，如果我们看不到输出，我们如何知道它正在运行呢？在看不到输出的情况下判断 SQLi 是否有效的一种方法是使用计时方法。这被称为盲注 SQL 注入（blind SQLi），我们看到可以使用 `ping` 命令。但为什么要用 `ping`？它默认每秒发送一个包。因此，如果我们发送五个包，预计脚本执行将挂起 5 秒。让我们使用 `xp_cmdshell` 语法构建一个新的 SQLi 字符串。

```
' or l=1; exec xp_cmdshell 'ping -n 5 127.0.0.1' --
```

当我们运行查询时，脚本完全没有挂起。我们尝试的是调用 `xp_cmdshell` 存储过程来 ping `127.0.0.1` 五次，导致脚本等待 5 秒。遗憾的是，`xp_cmdshell` 未启用。希望我们是以管理员用户登录的。如果不是，我们将寻找其他方法来利用这台机器。为了检查我们是否为管理员，我们修改了注入字符串。

```
' or l=1; if is_srvrolelemember('sysadmin') > 0 wait for delay '0:0:5' --
```
