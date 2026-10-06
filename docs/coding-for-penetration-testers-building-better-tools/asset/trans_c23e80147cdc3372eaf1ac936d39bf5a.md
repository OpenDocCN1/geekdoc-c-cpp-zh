

# 入口

为了利用我们任何 PowerShell 的强大功能，我们首先需要找到进入系统的方法。根据我们在进入机器后具体想要做什么，我们可能还需要管理员访问权限。有很多任务我们仅使用标准用户账户的权限就可以完成，例如 ping 扫描或端口扫描，因为这些任务只需要任何账户都拥有的普通访问级别。为了更改设置或在系统上执行我们可能需要的任何操作，我们通常在 PowerShell 中需要相同的访问权限。

在本章中，我们将查看如何通过 Windows 远程管理接口 WinRM 与 PowerShell 交互。我们能够在我们的测试系统上设置 WinRM，但许多企业系统已经安装了它。一旦设置完成，我们将查看如何从 Kali 与其交互。

# 设置 Windows 10 系统

在可以使用 PowerShell 渗透我们的系统之前，我们首先需要对我们的独立 Windows 10 工作站启用远程管理。为了做到这一点，我们需要启用 WinRM，即 Windows 远程管理接口。

```
winrm quickconfig
rm set winrm/config/service/auth '@{Basic="true"'
rm set winrm/config/client/auth '@{Basic="true"'
rm set winrm/config/service '@{AllowUnencrypted="true"'
-Item WSMAN:\localhost\TrustedHosts -value ""
```

这些命令将配置 WinRM，然后设置一些通常不需要设置的覆盖项。这些命令允许我们像作为域中受信任主机的一部分一样与 WinRM 交互。通常情况下，如果我们要与这些服务之一进行交互，我们本被允许作为域的一部分使用 Kerberos 身份验证，但由于我们没有域，我们必须“作弊”一下。

现在，我们需要设置我们的 Kali 镜像以便能够与 WinRM 交互。我们将使用一个名为“pywinrm”的 Python 模块。要安装它，我们在 Kali 中执行命令 `pip install pywinrm`，我们将去获取所需的。

接下来，我们想要构建一个示例脚本来验证是否可以连接。我们希望能够验证我们既可以连接又能执行 PowerShell 脚本。

```python
#!/usr/bin/python
import winrm
# 在此处放置脚本
script = "whoami"
ses = winrm.Session('<host IP>', auth=('<username>,<password>'))
r = ses.run_ps(script)
print r.std_out
print r.std_err
```

此脚本从导入 winrm 命令开始，以便我们能与远程 Windows 10 系统交互。然后我们创建脚本，该脚本仅包含 "whoami" 命令，用于打印我们以什么身份通过验证。最后，我们使用 Session 命令创建一个新会话。该会话随后用于运行我们的脚本，返回信息存储在我们的返回变量 "r" 中。此返回变量包含关于所运行命令的三个信息：status_code（状态码）、std_out 输出和 std_err 错误输出。我们打印 std_out 的输出以及发生的任何错误。我们将脚本保存为 "connect.py"，并在运行时运行它。

