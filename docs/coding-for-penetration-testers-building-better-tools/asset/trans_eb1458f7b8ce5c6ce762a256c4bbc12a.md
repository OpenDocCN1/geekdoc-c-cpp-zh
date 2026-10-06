
你正在运行的脚本始终位于 `sys.argv[0]`。在这个脚本中，我们的其他参数是我们要连接的主机（host）和端口（port）。如果缺少这些参数，我们就抛出一个错误并退出脚本。Python 允许用一行代码完成操作。除非另有指定，否则 `sys.exit` 的返回码假设为 0（无错误）。在这种情况下，我们要求它显示错误，由于我们执行了此操作，Python 将假设它应该返回代码 1（遇到错误）。如果我们想创建自定义错误代码，可以在此函数中使用任何数字。

一旦我们将剩余的项目分配给连接到我们的服务器，并请求我们的 URL。`client.get()` 方法会检索一个对象，该对象包含了我们的响应码、状态原因以及获取我们请求的网页正文的其他方法。我们想要确保返回的页面是 200 消息，这表示一切执行执行成功。如果我们确实收到了 200 消息，我们就打印站点正常并成功退出脚本。如果我们没有收到 200 状态，我们想要打印站点已宕机并说明原因。注意，我们在这里没有给 `sys.exit()` 传递数字。它应该假设 OK 时为 0。然而，良好的做法是不做假设，并养成始终输入数字的习惯。`resp.status` 将包含我们的返回码，而 `resp.reason` 将解释为什么是该返回码。这将让我们知道站点已宕机。

如果我们想监控一个站点以确保它在测试期间保持运行状态，可以使用 `watch` 命令。为了每 5 秒更新一次，我们将指定 `-n` 参数并将值为 5。请查看图 2.4 作为示例。

```
root@mostdefinitelykali:~/Desktop# ./webCheck.py happypacket.net 80
happypacket.net :~ OK
root@mostdefinitelykali:~/Desktop# _
```

# 图 2.4 使用 argv 运行 webCheck.py。

当我们使用 ARGV 时，必须按照特定顺序提供参数，并且必须处理所有的错误检查以及为我们的变量赋值。`optparse` 模块提供了一个名为 `OptionParser` 的类，可以帮助我们解决这个问题。让我们通过修改 `webCheck.py` 来研究 `OptionParser`：

```python
#!/usr/bin/python
import httplib, sys
from optparse import OptionParser
usageString = "Usage: %prog [options] hostname"
parser = OptionParser(usage=usageString)
parser.add_option("-p", "--port", dest="port", metavar="PORT", default=80, type=int, help="Port to connect to")
(opts, args) = parser.parse_args()
if len(args) < 1:
    parser.error("Hostname is required")
host = args[0]
#this is where the rest of webcheck.py begins
```

从这里开始，脚本的其余部分相同。我们首先从 `optparse` 模块导入 `OptionParser` 类。我们创建了一个可以传递给解析器的用法语句，然后定义解析器并将该语句作为用法选项传递。。我们可以直接传递给解析器而不先将其赋值给变量，但使用变量既更易读，又允许我们在需要时在其他地方复用该用法语句。如果带有 `-h` 标志运行脚本，`OptionParser` 将显示我们的用法语句。

由于大多数 Web 服务运行在 80 端口，我们可能并不总是每次使用脚本时都输入端口。因此，我们添加了一个选项，允许我们在命令行上指定端口。我们告诉解析器，`-p` 和 `-port` 都可以用于指定端口。`Metavar` 告诉我们 `-p` 或 `-port` 标志所需的参数，而 `help` 标志定义了详细帮助帮助的帮助文本。默认变量值在我们不使用默认值时将在其中存储一个不同的值。注意此行后的缩进。缩进告诉解释器我们正在继续之前的语句。这允许我们拆分行，使代码更具可读性。

现在选项已经设置好，我们调用解析器类的 `parse_opts` 方法。输出设置两个变量：`opts` 和 `args`。`opts` 通过我们指定的选项设置，而 `args` 是传递到命令线的其他内容，在这种情况下是我们的主机名。从这里开始，其他所有工作都相同，不同之处在于主机和端口值的来源。我们的主机是 `args` 列表中的第一个项，我们可以直接从 `opts` 对象指定端口。

让我们测试一下新程序。看看图 2.5。

![](img/42f332b2adf7dab7e681e5d6cdd2074c_84_0.png)

# 图 2.5 使用 OptionParser 运行 webCheck.py。

# 列表

假设我们需要将无类网间域路由（CIDR）格式的 IP 地址转换为 IP 范围和子网掩码。CIDR 格式是表示 IP 地址信息的一种。它没有列出完整的网络信息，而只有 IP 地址和子网掩码的位数。有几种方法可以做到这一点。我们可以手动计算、使用子网计算器，或编写脚本。由于你正在读一本脚本书，我们应该使用脚本。这将为我们一个探索列表的机会。列表是 Python 版本的数组。它们拥有自己方法的对象。让我制作这样的：

```
root@bt:~ ./subcalc.py 192.168.1.1/24
```

首先，我们想要将输入 (192.168.1.1/24) 拆分为 CIDR 和 IP 地址以便单独处理。

```python
addrString,cidrString = sys.argv[1].split('/')
```

`split` 方法始终返回一个列表。在这种情况下，我们的列表有两个值：IP 地址（我们将其放入 `addrString` 变量）和 CIDR 表示法（我们将其放入 `cidrString` 变量）。我们告诉 `split` 使用斜杠来确定将字符串拆分为我们的列表元素。

现在我们想要对我们的 IP 地址执行类似的操作以便单独解析每个字节节：

```python
addr = addrString.split('.')
```

这次我们使用句号作为分隔符，并使用 `addr` 来存储我们的字节节列表。但有一个问题。我们有一堆字符串。我们将不得不……
（注：OCR 文本截断或重复。我们将根据提供的逻辑进行重构。）
