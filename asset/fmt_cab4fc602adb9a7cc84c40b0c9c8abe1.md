
在第一行中，我们连接到数据库。构成查询的每一行都会在 `GO` 命令后执行。`-S` 参数是服务器名称，`-E` 表示我们使用受信任连接登录，`-d` 指定数据库。要使用 `sqlcmd`，你必须指定 `exit`。注意所有参数对大小大小敏感。如果你不在受信任连接上且想使用用户名和密码，可以使用以下命令。

### 代码列表 94：使用 SQL Server 登录的 `sqlcmd`

```
sqlcmd -S [servername][instancename] -U username -P password -d
AdventureWorks2014
```

当你从命令提示符运行 `sqlcmd` 时，你可以将查询跨越多行并使用 `GO` 执行。当你不在命令提示符中时，你需要使用 `-q`（查询）或 `-Q`（查询并退出）以及单行查询语句。

### 代码列表 95：使用直接查询命令的 `sqlcmd`

```
sqlcmd -S [server\instance] -E -d AdventureWorks2014 -Q "SELECT * FROM Person.Person WHERE BusinessEntityID = 1"
```

当然，你也可以使用 `-i` 指定要运行的脚本文件。在某处创建一个文件（我把它放在了 `C:\Temp`），命名为某个名称（`SelectPerson1.sql`），然后你就可以运行以下命令。

### 代码列表 96：使用输入文件的 `sqlcmd`

```
sqlcmd -S [server\instance] -E -d AdventureWorks2014 -i C:\Temp\SelectPerson1.sql
```

现在结果在命令提示符中可能有点难读。你也可以使用 `-o` 将它们输出到文件中。

### 代码列表 97：使用输出文件的 `sqlcmd`

```
sqlcmd -S [server\instance] -E -d AdventureWorks2014 -i C:\Temp\SelectPerson1.sql -o C:\Temp\result.txt
```

你可能喜欢的使用的另一个选项是 `-b`，它会在发生错误时终止作业。你可以在 `sqlcmd` 文中找到所有选项。

使用 `sqlcmd`，你可以通过从命令行运行来自动化某些 SQL 任务。我应该提到的是，这完全不能替代 `SQL Agent`，后者也可以运行自动化的 SQL 作业。问题在于，你无法从 `CI` 工具运行 `SQL Agent`，但你可以运行 `sqlcmd` 实用程序。`sqlcmd` 工具仍然没有自动化你的部署，但它可能对于测试开始之前或将新脚本提交到版本控制系统之后自动运行脚本有用。

# 结

书中介绍的工具不会让你成为最优秀的 `C#` 开发者，也不会教你如何成为一名出色的 `DBA`。它们为你提供了两者的折中方案。我见过许多缺乏基本数据库技能的开发者。`SQL` 注入仍然发生得频繁。由于 `SQL` 查询完全不理想，软件在生产一年后会变得缓慢。公司不得不投资昂贵的服务器硬件，是因为开发者在循环中放置了查询、对 `ORM` 的懒加载功能感到惊讶，或者仅仅是编写了极其糟糕的 `SQL` 查询。虽然这本书在编写查询方面对你帮助不大，但它可能帮助你对整个数据库有一个更宽广的视角。参数化你的查询，但要小心参数嗅探（`parameter sniffing`）。要清楚你一个运行五分钟的查询可能会阻塞整个系统。识别这些瓶颈并修复，或者防止它们发生。
