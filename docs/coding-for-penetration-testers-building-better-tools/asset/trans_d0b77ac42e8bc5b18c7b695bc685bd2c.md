
Windows API 中的函数。

本章重点介绍 PowerShell 在某些渗透测试场景下如何派用场。在讨论了执行策略以及绕过这些策略的代码后，本章将讨论如何进入系统，以及进入系统后可以使用 PowerShell 执行哪些操作。它涵盖了 PowerShell 的一些示例用法，例如控制进程和服务、与事件日志进行交互、在网络上获取和发送文件，以及与注册表交互，最后以使用 PowerShell 和 Metasploit 攻击框架可以完成的操作示例作为结语。

在第 1 节“命令行脚本介绍”中，我们花费了大量时间讨论微软的 PowerShell 以及我们如何使用它来开发 shell 脚本。其中某些脚本如果进一步开发，对于通用任务可能有用，例如收集主机及其所在网络上的信息。在本章中，我们将直接深入研究 PowerShell 作为黑客工具的细节。

直到很最近，PowerShell 还不被普遍认为是一种可以用于攻击的工具。正如我们在第 1 节“命令行脚本脚本介绍”中讨论的，它拥有一套非常严格的权限，限制了我们在系统上运行的内容，我们必须放这些权限才能运行最基本的脚本和命令。此外，如果我们不采取禁用这些安全措施的步骤，确实无法在系统上使用 PowerShell 做什么……以前是这样认为的。

在 2010 年的 DEF CON18 上，David Kennedy 和 Josh Kelley 发表了关于 PowerShell 的演讲 [1]，讨论了它可能如何作为攻击工具使用、我们如何绕过现有的安全措施，以及我们可以将 PowerShell 用于渗透测试场景的某些有趣用法。鉴于 Kennedy、Kelley 以及其他在该演示中讨论的代码的工作人员所付出的努力，我们现在更有可能以新颖且的方式使用 PowerShell。让我们开始吧，看看能让 PowerShell 为我们做些什么。

## 处理 PowerShell 中的执行策略

正如本章提到的以及在第 1 节“命令行脚本介绍”中讨论的那样，存在规定我们在 PowerShell 中可以做某些事的执行策略。在第 1 节“命令行脚本介绍”中，我们必须将执行策略更改为 RemoteSigned 才能运行我们的脚本，但我们并没有真正讨论过具体的策略，或者每种策略的具体作用是什么。我们现在来回顾一下。

### 执行策略

有五种执行策略：Restricted、AllSigned、RemoteSigned、Unrestricted 和 Bypass。Restricted 策略（也是默认执行策略）阻止我们运行任何 PowerShell 脚本，但允许我们交互式使用 shell。AllSigned 策略允许我们运行由受信任发布者数字签名的脚本。RemoteSigned 策略允许我们运行自己创建的脚本，但我们下载的脚本必须经过受信任发布者的数字签名。Unrestricted 策略没有任何限制，允许我们运行任何来源的未签名脚本，但当脚本从互联网下载时会发出警告。Bypass 策略允许我们从任何地方运行脚本，并且会在不考虑来源的情况下执行脚本。这些执行策略可以按照我们在第 1 节“命令行脚本介绍”中讨论的方式进行更改。

某些执行策略所涉及的“签名”是指脚本本身的数字签名。这些签名必须来自受信任的发布者，以符合各种执行策略的要求。

### 提示

我们实际上可以创建一个自签名证书来为我们的脚本签名，但在脚本运行时（至少是第一次运行时）我们仍会警告。这是一个有些复杂的过程，但互联网上有相关的文章和教程可以指导我们完成它¹。在渗透测试中，我们通常直接绕过执行策略会更好，正如我们将在“绕过策略”章节中讨论的那样。

> ¹http://www.hanselman.com/blog/SigningPowerShellScripts.aspx。

在理想世界中，我们希望执行策略被设置为 Unrestricted、Bypass 或至少是 RemoteSigned，以便我们就能在目标系统上运行脚本。然而，正如我们在第 1 节“命令行脚本介绍”中讨论的，如果执行策略尚未按此方式设置，则我们需要对系统进行一些更改。在渗透测试中，我们可能不想更改系统中的设置。坦率地说，有一种解决此问题的方法完全不需要任何更改，就能让我们运行任何我们喜欢的脚本。

## 绕过策略

为了绕过管理 PowerShell 的执行策略所实施的限制，我们可以使用 Peters、Kelley 和 Kennedy 开发的 CreateCMD 代码 [2]。下面的示例是上述作者开发的相同代码，为了简洁起见，去了一些注释和用法。

```query
param($Filenames);
if (-not $Filenames)
{
    Write-Host "Usage: createcmd.ps1 [-Filenames] <string[]"
    return;
}
$contents = gc $Filenames;
$ms = New-Object IO.MemoryStream
    $cs = New-Object IO.Compression.DeflateStream ($ms, IO.Compression.CompressionMode]::Compress)
    $sw = New-Object IO.StreamWriter ($cs,[Text.Encoding]::ASCII);
    $contents | % {
        $sw.WriteLine($_);
    }
}
$sw.Close();
```

```query
$code = [Convert]::Base64String($ms.ToArray());
$command = "Invoke-Expression `$(New-Object IO.StreamReader (\
  `$(New-Object IO.Compression.DeflateStream (\
    $,([Convert]::FromBase64String(`$code`)),
    [IO.Compression.CompressionMode]::Decompress))\n  ), [Text.Encoding]::ASCII)).ReadToEnd())` Load complete.\`"
$command = "powershell.exe "[1]"";
$command -f "Command",command.Replace("\", ""\\")
```

让我们快速看一眼我们在做什么。第一行接收脚本的参数，使用我们在 `param` 中使用的方法来创建。这本质上与我们在第 1 节“命令行脚本介绍”中使用的方法相同，但代码稍少一些。在这种情况下，我们从命令行获取文件名。我们使用 `gc`，它读取 `$Filenames` 中的文件内容（非常像 Linux 中的 `cat`），并将它们放入 `$contents`。变量 `$ms` 是 `IO.MemoryStream` 对象的句柄，稍后我们将用它来进行存储。我们分别将 `$cs` 和 `$sw` 设置为 `IO.Compression.DeflateStream` 和 `StreamWriter` 对象的句柄。一旦设置好所有对象，我们将压缩后的内容写入内存流并关闭流写入器。

现在我们的脚本内容已存储中，我们可以对它们进行转换。`$ms` 的 Base64 转换字符串被赋值给变量 `$code`。这是我们在 shell 上下文中传递给 `Invoke-Expression` 的代码。

最终，我们将通过 `fileout.ps1 | Out-File fileout.bat ascii` 运行 `createcmd.ps1`。我们的测试脚本 `fileout.ps1` 应该只包含 `Set-Content -Encoding utf8 test.txt "test"` 这一行，这将输出一个文件，以便我们有结果可以查看。我们最终将得到一个 `fileout.bat` 文件，运行时将执行我们的原始代码。这段代码允许我们完全绕过执行策略并执行我们的代码，无论来源是什么，无论执行策略级别设置到多少。为了说明清楚，我们实际上并没有更改执行策略级别，也没有在系统中进行任何配置更改。我们仅仅是绕过了针对签名脚本的安全措施。

## 警告

目前，CreateCMD 代码运行良好，可以帮助我们绕过微软作为安全措施对 PowerShell 脚本施加的策略限制。当然，我们无法保证这种情况会持续下去，无法保证微软不会发布补丁或关闭此特定漏洞的新 PowerShell 版本。如果我们发现 CreateCMD 代码完全失效，或者在某些 PowerShell 版本上不起作用，可能值得检查一下是否真的发生了这种情况。
