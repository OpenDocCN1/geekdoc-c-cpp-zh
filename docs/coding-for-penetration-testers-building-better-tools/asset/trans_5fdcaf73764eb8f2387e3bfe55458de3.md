
我们将使用 `Etc` 模块的 `getpwuid` 方法将我们的 uid 转换为用户名。`getpwuid` 返回来自密码文件中关于该 uid 的信息。我们需要的唯一字段是 `name`，因此我们引用返回的密码结构中的 `name` 变量。为了能够读取其他用户拥有的进程并测试此程序，我们需要 root 权限。作为 root，我们运行脚本 `proc.rb`，其进程 ID 为 `i`，我们应该会在图 4.6 中看到输出。

```
File Edit View Search Terminal Help
root@kali:~ ruby proc.rb 1
Process 1 is owned by root
Process 1 CWD: /
Process 1 Command: /sbin/init
root@kali:~# 
```

# 图 4.6 使用 proc.rb 确定进程信息。

# 数据库基础

在 Ruby 中，即使是数据库记录也可以视为对象。`Active Record` 是一个为 Rails 框架设计的 Ruby 模块。它旨在抽象数据库内部细节。使用 Active Record 构建程序时，在某些情况下我们甚至不需要知道数据库的结构。与其处理复杂的 SQL 查询，`Active Record` 让我们像对待类一样对待数据库信息。我们可以使用这些 Active Record 模型连接到数据库服务器并查询记录，而没有大量的开销。如果在渗透测试期间遇到凭据，我们可以很容易使用 Ruby 将数据从数据库获取到可以轻松传输回系统的格式中。

为了演示，我们需要一个数据库服务器和一个用户。Kali 安装了 PostgreSQL 以供 Metasploit 使用。利用这一点来完成这些示例。开始之前，我们必须验证数据库服务器正在运行。要做到这一点，我们需要检查服务器状态，如果它没有运行，则启动它。我们需要变成 `postgres` 用户并为我们的使用创建一个用户和数据库。

```
service status
postgresql.service - PostgreSQL RDBMS
Loaded: loaded - /(lib/systemd/system/postgresql.service;
(disabled)
Active: inactive (dead)
root@kali:~# echo -e "local test test md5\nlocal all all ident" >/etc/postgresql/9.4/main/pg_hba.conf
root@kali:~# service postgresql start
root@kali:~# su postgres
postgres@kali:~$ createuser --interactive -P test
Enter password for new role: test
Enter it again: test
Shall the new role be a superuser? (y/n) n
Shall the new role be allowed to create databases? (y/n) y
Shall the new role be allowed to create more new rules? (y/n)
y
postgres@kali:~$ createdb --owner test test
postgres@kali:~$ exit
logout
root@kali:~# apt-get install postgresql-server-dev-9.4
[output suppressed for brevity]
root@kali:~# gem install dbi
Fetching: deprecated-2.0.1.gem (100%)
Successfully installed deprecated-2.0.1
Fetching: dbi-0.4.5.gem (100%)
Successfully installed dbi-0.4.5
Parsing documentation for dbi-0.4.5
Installing ri documentation for dbi-0.4.5
Parsing documentation for deprecated-2.0.1
Installing ri documentation for deprecated-2.0.1
Done installing documentation for dbi, deprecated after 0 seconds
2 gems installed
root@kali:~# gem install pg
Building native extensions. This could take a while...
Successfully installed pg-0.18.4
Parsing documentation for pg-0.18.4
Installing ri documentation for pg-0.18.4
Done installing documentation for pg after 1 seconds
1 gem installed
```

# 使用 DBI

现在我们的数据库已经准备好了，我们可以查看一些有趣的部分。`DBI` 模块允许我们连接并操作数据库，同时抽象了许多特定的数据库方面。

让我们看看如何连接到新创建的 PostgreSQL 实例。

```ruby
#!/usr/bin/ruby
require 'dbi'
dbh.connect('DBI:Pg:test', 'test', 'test')
dbh.do("set client_min_messages = 'warning'")
```

我们将包含 DBI 模块并使用 `connect` 方法。我们的连接选项是连接字符串，它由 `DBI`、数据库驱动（在此情况下是 PostgreSQL 的 `Pg`）和数据库名称 `test` 组成。第二个选项是用户名，第三个也是密码 `test`。`connect` 方法返回一个数据库句柄。我们将其简写为 `dbh`。我们使用数据库句柄调用 `do` 方法，该方法会在数据库上运行我们传递给它的字符串。在这种情况下，我们传递了一个将禁用我们预期的某些警告信息的字符串。这将清理输出，且脚本仍将正常运行。

接下来，我们需要创建表。我们将 SQL 语句添加到一个字符串中，并在数据库上执行该字符串。首先我们创建一个语句处理器，然后执行该处理器。在在此此之前，如果表已存在，我们应该删除它，以便我们通过第一个脚本获得可的可重现的结果。

```ruby
db_create = '
create table people (
id SERIAL,
name varchar(256),
homepage varchar(256)
)'
dbh.do('drop table if exists people')
q = dbh.prepare(db_create)
q.execute()

qstring = "  insert into people (name,homepage)\nvalues('ryan','http://www.happypacket.net')"
dbh.prepare(qstring).execute()
qstring = "  insert into people (name,homepage)\nvalues('jason','http://www.codingforpentes.net')"
dbh.prepare(qstring).execute()

# (此处由于原文中存在大量重复和混乱文本，已根据逻辑进行了清理和翻译)
