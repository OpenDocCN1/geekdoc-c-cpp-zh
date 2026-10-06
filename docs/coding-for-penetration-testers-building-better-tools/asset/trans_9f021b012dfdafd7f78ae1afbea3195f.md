

然后我们使用 `Where-Object` 来显示匹配我们传递给它的条件的输出。我们通过 `state` 过滤输出，只显示状态为“Running”（运行）的进程。最后，我们使用 `Select` 将输出限制为我们感兴趣的字段并将其打印。当我们将其保存为 `getServices.py` 并运行时，我们应该能看到像图 6.4 所示的输出。

文件 编辑 查看 搜索 终端 帮助

```
root@kali:~# python getServices.py
```

| Name | State | Status |
| :--- | :--- | :--- |
| Appinfo | Running | OK |
| AudioEndpointBuilder | Running | OK |
| Audiosrv | Running | OK |
| BFE | Running | OK |
| BITS | Running | OK |
| BrokerInfrastructure | Running | OK |
| Browser | Running | OK |
| Bserv | Running | OK |
| COMSysMessagingRegistrar | Running | OK |
| Crypto | Running | OK |
| DcomLaunch | Running | OK |
| DeviceAssociationService | Running | OK |
| DeviceInstall | Running | OK |
| Dhcp | Running | OK |
| DiagTrack | Running | OK |
| Dhcache | Running | OK |
| ppcs | Running | OK |

# 图 6.4 getServices.py 的输出。

如果我们想控制服务，也可以通过 PowerShell 来实现。我们可以分别使用 `Start-Service`、`Stop-Service` 或 `Restart-Service` 来启动、停止或重启服务。通常情况下，我们需要管理员权限来操作服务。

## 与事件日志交互

在 PowerShell 中处理事件日志是一项项非常容易的任务。微软已经提供了一个简单的接口来处理它们，尽管存在一些局限性。同样，我们将像在本节之前处理进程那样，查看如何在 PowerShell 交互模式下处理事件日志。

我们在目标系统上对事件日志最想做的操作可能是查看系统上有什么内容。为此，我们可以使用 `Get-EventLog` cmdlet 配合 `list` 参数，如 `Get-EventLog -List`。当我们运行此 cmdlet 时，应该会看到与图 6.5 所示类似的输出。

![](img/42f332b2adf7dab7e681e5d6cdd2074c_250_0.png)

# 图 6.5 getEvents.py 的输出。

一旦我们有了事件日志列表，可以使用相同的 cmdlet 配合不同的参数来列出特定日志的内容。当我们查看特定系统上的日志时，其中很可能包含大量信息，除非我们要将日志内容导出到文件，否则我们也想过滤返回给我们的内容。我们可以通过使用 `Get-EventLog` 的 `-newest` 参数来获取指定日志的最后几条消息，导入 winrm

```python
import winrm
# Place Script Here
script = ""
Get-EventLog -List | ForEach-Object { Get-EventLog $_.Log -Newest 10 }

s = winrm.Session('172.16.85.130', auth=('sussurro','Abc123!'))
r = s.run_ps(script)
print r.std_out
```

我们对脚本进行了扩展，使其使用 `ForEach-Object` cmdlet。该 cmdlet 将获取上一个命令的输出行并对其执行操作。在这个示例中，我们告诉它从找到的列表中获取每个事件日志的最新 10 个项目。这应该可以获取 event\log 中每个日志的最新 10 个事件。当我们运行此脚本时，它看起来应该类似于图 6.6。

```
runhell= -python getEvents.py
Index  EntryType Source                     InstanceID Message
2087 Feb 00 06:22  Information-Microsoft-...    4097 Successful auto update of third-party root...
2088 Feb 00 06:22  Information-Microsoft-...    4097 Successful auto update of third-party root...
2089 Feb 00 06:23  Information-Microsoft-...    4097 Successful auto update of the-service...
2884 Feb 00 06:22  Information-Microsoft-...    4097 Successful auto update of third-party root...
2882 Feb 00 22:30  Information-Microsoft-...    4097 Successful auto update of third-party root...
2883 Feb 00 06:23  Information-Microsoft-...    4097 Successful auto update of third-party root...
2089 Feb 00 06:10  Information-Microsoft-...    4097 Successful auto update of third-party root...
2760 Feb 00 19:01  Information-Microsoft-...    4638 An account was logged off.
1559 Feb 00 07:04  Information-Protection-...    10737 The Protection service has been stopped.
1560 Feb 00 07:04  Success-Protection-...    4638 An account was logged off.
1558 Feb 00 07:04  Success-Microsoft-...    4638 An account was logged off.
1558 Feb 00 07:04  Success-Microsoft-...    4626 An account was logged off, referred to new domain, as in
1558 Feb 00 07:04  Success-Microsoft-...    4624 An account was successfully logged on., as in
1499 Feb 00 06:04  Information-Microsoft-...    4624 A logon was attempted with explicit credential...
```

# 图 6.6 使用 getEvents.py 查看事件日志。

我们也可以使用 `Clear-EventLog` cmdlet 轻松地清除事件日志。要做到这一点，我们需要指定想要清除的日志以及该日志所在的系统名称，如 `Clear-EventLog Application`。这是我们需要作为管理员才能运行此特定 PowerShell 代码的区域之一。如果我们不是管理员，将收到“拒绝访问”错误消息。通过 WinRM 运行具有某些优势，而登录控制台的用户可能无法这样做，但 WinRM 将允许我们删除日志。

在这里我们再次获取列表，并对每个对象清除事件日志。然而，在我们运行期间，我们将生成一些额外的特性。当 WinRM 登录和注销系统时，它会生成日志，当 PowerShell 时会生成额外的日志。让我们看看清除日志并重新检索生成了什么。当我们运行 `clearEvents.py` 然后运行 `getEvents.py` 时，我们看到了许多条目，包括日志清除的地方以及我们重新登录 PowerShell 的地方。这可以在图 6.7 中看到。

```
rootall: # python clearEvents.py
rootall: # python getEvents.py
```
| Index | Time | EntryType | Source | InstanceID | Message |
|---|---|---|---|---|---|
| 1668 07 00:29 | Success | Microsoft-Windows... | | 4623 An account was logged off. |
| 1669 07 00:29 | Success | Microsoft-Windows... | | 4624 An account was logged off. |
| 1670 07 00:29 | Success | Microsoft-Windows... | | 4624 A service was assigned to new log. |
| 1671 07 00:29 | Success | Microsoft-Windows... | | 4624 An account was successfully logged on. |
| 1672 07 00:29 | Success | Microsoft-Windows... | | 4624 User logon using explicit credential. |
| 1673 07 00:29 | Success | Microsoft-Windows... | | 4672 Special privileges assigned to new log. |
| 1674 07 00:29 | Success | Microsoft-Windows... | | 4624 An account was successfully logged on. |
| 1675 07 00:29 | Success | Microsoft-Windows... | | 4624 Logon was attempted using explicit credential... |
| 725 07 00:29 | Information | Information Windows | | 4624 Logon attempted using explicit... |
| 719 07 00:29 | Information | Microsoft-Windows... | | 104 The SpurPrint Diagnostics log file was cleared. |
| 718 07 00:29 | Information | Microsoft-Windows... | | 104 The System log file was cleared. |

