

```python
script = """
$src = "http://nmap.org/dist/nmap-7.01-setup.exe"
$dest = "c:/Windows/temp/nmap-7.01-setup.exe"
$web = New-Object System.Net.WebClient
$web.DownloadFile($src, $dest)
ls c:/windows/temp/nmap*
"""

ses = winrm.Session('<remote IP>', auth=
('<username>','<password>')
r = ses.run_ps(script)
print(r.std_out)
```

让我们快速查看一下我们在这里所的操作。首先，我们将文件的 URL 赋值给 `$src` 变量。我们还需要指定要保存文件的位置。我们将将其保存到 "C:/Windows/temp" 下的 Windows 临时目录。当我们在 PowerShell 中指定路径时，我们使用 `/` 路径语法，因为 `\` 是转义字符。

接下来，我们实例化用于与 Web 接口的对象 `System.Net.WebClient`，并使用 `$web` 作为它的句柄。这将允许我们与网站进行交互。`WebClient` 接口有多种不同的检索和上传数据的方法，但我们使用了 `DownloadFile` 方法。我们为 Web 对象指定句柄，并传递我们正在下载的 URL 以及我们想要存储的位置，例如 `$web.DownloadFile($url, $path)`。这是处理 Windows 机器上 Web 流量的一段非常简单的代码。当我们运行脚本时，我们应该看到类似于图 6.8 的所示输出。

```
root@kali:~# python getfile.py

Directory: C:\windows\temp

Mode                LastWriteTime             Name
-a----        2/8/2016  2:11 PM    26387073 nmap-7.01-setup.exe
```

# 图 6.8 运行 getfile.py 以检索 Nmap。

我们可以使用许多非常实用的对象和方法来处理其他类型的事务和流量。对于 `System.Net.WebClient`，我们还可以利用 `UploadFile` 方法向另一个方向发送文件，在我们查看 Web 事务时，这可能对我们非常有用也可能没，但我们也可以使用 `System.Net.WebClient` 执行 FTP，而不需要任何重大更改。

```python
import winrm
# 在此处放置脚本
script = """
src = "c:/Windows/tmp/nmap-7.01-setup.exe"
dest = "ftp://192.168.1.54/upload/nmap-7.01-setup.exe"
$web = New-Object System.Net.WebClient
$web.UploadFile($script, $dest)
"""
ses = winrm.Session('172.16.85.130', auth=('sussurro','Abc123!'))
r = $ses.run_ps(script)
print r.std_out
```

当然，这与我们刚刚看到的 Web 下载非常相似，这是合逻辑的，因为我们使用了相同的对象和相同的方法。由于我们执行的是非常相同的事务，唯一的实际区别在于文件的目标是一个 FTP URI。我们可以使用此模块使用 FTP、HTTP 或 HTTPS，如果我们的脚本运行在代理之后，我们还可以指定代理信息。`System.Net.WebClient` 已经在内部透明地为我们处理了所有的协议差异。

正如我们在第 1 章“命令行脚本简介”中讨论的那样，我们可以访问 .NET 中海量的对象，其中许多与网络相关。在许多情况下，我们可以找到对于在网络中传输文件时可能想要执行的大多数常见任务的现有对象和方法。对于我们无法使用其中任何一个来适应的特殊情况，互联网上有大量的用户生成代码供我们使用和构建。此外，我们还可以访问通过操作系统或具有命令行界面的已安装应用程序可用的任何其他功能。

# 提示

任何从未遇到过 Netcat 的人都错过了一个具有极高灵活性的重要渗透测试工具。Netcat 适用于许多操作系统，我们可能在某些操作系统的安装中作为默认安装的一部分找到它。Netcat 本质上允许我们处理入站和出站网络流量（或两者），并从我们可能关心的任何端口在网络上移动文件或数据。我们可以在 https://github.com/besimorhino/powercat 找到 Netcat 的 PowerShell 重现。

鉴于如 Netcat 这样的工具（我们可以为 Windows 操作系统下载并通过 PowerShell 轻松控制它），我们可以在网络上移动文件、打开 shell 或反向 shell，并执行一系列类似的任务。

# 与注册表交互

微软操作系统中的注册表（最早于 Windows 3.1 引入）是一个存储微软操作系统及其安装的应用程序的配置设置的数据库。我们可以使用注册表来操作应用程序的运行方式（或保持其运行）。

注册表是层次结构的，通常以一系列文件夹的形式呈现。在注册表层级的每个层级中，我们可以发现“值”（values），它们包含名称和关联数据。在注册表中，我们可以发现五个主要部分，被称为“配置单元”（hives）：

- HKEY_LOCAL_MACHINE (HKLM) 用于本地机器设置
- HKEY_CURRENT_CONFIG (HKCC) 系统启动时生成
- HKEY_CLASSES_ROOT (HKCR) 关于应用程序的信息
- HKEY_USERS (HKU) 用户的总集
- HKEY_CURRENT_USER (HKCU) 关于当前登录用户的设置

PowerShell 以文件系统的方式向我们展示注册表，这是一个非常方便的界面。我们可以使用 `cd`（切换目录）命令来访问它，使用之前列出的缩写，例如 `cd HKLM`。当我们到达时，可以使用 `dir` 查看 HKLM 下的内容。我们应该看到类似于图 6.9 所示的输出。

```
File Edit Search Terminal
root@kali:~# python listHKLM.py
Hive: HKEY_LOCAL_MACHINE
Name Property
---- ----
BCD0000000
HARDWARE
SAM
SOFTWARE
SYSTEM
```

# 使用 PowerShell 列出 HKLM。

我们还还会看到一些关于 SECURITY 文件夹访问限制的错误，这对于从 Vista 开始的大多数系统是正常的。从这里，我们可以浏览 HKLM 下的部分。对于那些跳跃并尝试导航到所有配置单元的人，我们可能会发现其中两个是可以立即访问的：HKLM 和 HKCU。这些是 PowerShell 默认配置的唯一单元。坦率地说，我们可以轻松创建其他的：

```powershell
New-PSDRIVE -name HKCC -PSProvider Registry -Root HKEY_CURRENT_CONFIG
New-PSDRIVE -name HKCR -PSProvider Registry -Root HKEY_CLASSES_ROOT
```

为了创建这些额外的配置单元，我们不需要任何系统权限。在每个条目之后，我们应该能够切换到新的注册表配置单元并使用 `dir` 查看其内容，类似于图 6.6 所示。

当我们位于注册表结构所需的位置时，我们需要使用不同的命令来锁定键中的单个值。使用 `dir` 只会向我们显示层级中特定位置的子键，而不是值，这有点反直觉。

让我们快速查看注册表中的一些有趣的值。在大多数 Windows 操作系统中，如果在 HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run 中放置一个值，并且该值指向一个可执行程序，那么每当操作系统启动时，该程序就会被加载。当我们购买一台装满垃圾软件的新电脑时（所有软件在系统启动时都会加载），我们运行 `Get-ItemProperty "hklm:\software\microsoft\windows\currentversion\run"`，应该看到类似于图 6.10 所示的输出，尽管具体的条目会随机器而异。每一个这些值及其关联数据都指向文件系统中特定的安装应用程序或可执行脚本。

