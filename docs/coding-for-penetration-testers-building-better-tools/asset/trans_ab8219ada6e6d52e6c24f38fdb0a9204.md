
通过它们，例如 $i 或 $monkey；我们如何称呼它真的没有区别。

与我们之前的探测（pinging）程序相比，唯一的其他变化是将我们的 `ping.send` 目标更改为 $device，以匹配我们的 `foreach` 配置。

## 使用 PowerShell 整合一切

现在，我们将利用在本章中讨论过的各种 PowerShell 函数，并使用它们来组装一个小型的端口扫描工具，在此过程中我们还会添加一些新功能。这个工具远非完美，但在我们遍历代码时，将讨论潜在的问题，并讨论一些我们可以改进的领域以及我们可能如何实现这些改进。

## 使用 PowerShell 构建端口扫描器

我们开始构建端口扫描器。我们有两种用法可以来运行它。在扫描单个端口时，我们会运行类似于 `.\portscanner.ps1 scanme.nmap.org 80` 的命令。这会为我们检查 80 端口并退出。我们还可以使用 `.\portscanner.ps1 multi 80 85` 来指定端口范围。这将按顺序检查 80 到 85 端口。

```powershell
# 使用数组，我们可以按顺序获取参数
($device, $port, $start, $stop) = $args
#function pingdevice
# 探测设备以检查它是否在网络上
function pingdevice({
  if(test-connection $device -erroraction silentlycontinue){
    write-output "$device is up"
  }else{
    write-output "$device is down"
    exit
  }
}
#function checkpoints
# 检查我们的端口是否开放
function checkpoints{
  if ($port -match "multi") #此分支检查端口范围
```

```powershell
for ($counter=$start; $counter -le $stop; $counter++)
{
    write-output "testing port $counter on $device"
    $porttest = new-object Net.Sockets.TcpClient
    try{
        $connect = $porttest.connect($device,$counter)
        write-output "$counter is open"
    }catch{
        write-output "$counter is closed"
    }
}else{#此分支检查单个端口
    write-output "testing port on $device"
    $porttest = new-object Net.Sockets.TcpClient
    try{
        $connect = $porttest.connect($device,$port)
        write-output "$port is open"
    }catch{
        write-output "$port is closed"
    }
}

# 运行我们的函数
pingdevice
checkpoints
```

查看代码列表，我们可以看到本节中讨论的各种结构，以及为了多样性而加入的一些新东西。由于我们的脚本变得有点庞大，我们看到的第一个新东西是注释。我们可以使用 `#` 字符来表示我们不希望解释器对该行或该行的某部分执行任何操作。我们可以在行的开头或中间的任何位置放置注释标记，其后的所有内容都将被忽略。

脚本的下一行获取传递给脚本的任何参数，并将它们放入稍后使用的变量中。我们可以始终预期的 $device 变量是一个 IP 地址或域名，但其他三个变量可能会变化，或者完全不被使用，正如我们在其中一个函数中看到的那样。

`pingdevice` 函数将检查我们的 $device 变量中指定的 IP 或域名在网络上是否确实是连通的。该函数包含一个简单的语句，并使用 `test-connection` 命令来探测设备。我们在此处还使用了 `-erroraction` 参数，以便妥善处理设备实际上未连通时我们将得到的错误。这允许我们继续操作，如果在检查时没有在网络上发现任何内容，就不会向控制台输出错误。根据 `test-connection` 的结果，我们输出一条短消息，说明设备是连通还是断开。

我们的第二个函数实际上执行检查开放端口的工作。该函数有两个主要分支，一个用于检查单个端口，另一个用于检查多个端口。我们进入哪个分支取决于运行脚本时传递给脚本的参数。当我们在查看变量时也提到过，我们正在将其中一些变量用于不同的用途。

如果我们正在检查单个端口，我们将只使用前两个参数 `$args[0]` 和 `$args[1]`。在这种情况下，$args[0]` 将是我们的 IP 域名，$args[1]` 将是我们要检查的单个端口。如果我们正在检查多个端口，$args[0]` 将是我们的 IP 或域名，$args[2]` 和 `$args[3]` 应该是 `multi` 以指示多个端口，并且将分别是我们的起始和结束端口。如果脚本在来自 `$args[1]` 的 `$ports` 变量中看到值 `multi`，它将进入 `checkpoints` 函数中多端口的分支。

在脚本的任何分支中，我们都使用 `Net.Sockets.TcpClient` 来尝试连接目标端口。我们将进行一个快速而粗略的连接。
