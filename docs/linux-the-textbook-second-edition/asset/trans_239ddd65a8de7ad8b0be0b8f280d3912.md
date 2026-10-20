
## 18.5.2.1 在将 webserver2 设为服务之前如何运行它

在运行 webserver2 的目录中，你必须有一个有效的 index.html 文件。我们不提供 index.html 文件的创建方式，也不举例说明其创建过程，而是留给你自己去完成。

一旦你正确编译了 webserver2，就可以通过输入以下命令来运行它：

```
$ ./webserver2 port_number /pathname_to_web_directory
```

其中
port_number 是希望它监听的端口，例如 8083，
/pathname_to_web_directory 是存放可执行二进制映像和 index.html 文件的路径，例如 /home/bob

在我们的 Linux Mint 系统上运行它的命令是

```
$ ./webserver2 8083 /home/bob/index.html
```

请注意，webserver2 是一个静态页面服务器——它会向请求方发送任何以 .htm、.html、.jpg、.jpeg、.gif、.png、.ico 和 .zip 结尾的页面。它不支持运行通用网关接口（CGI）脚本、Perl 或超文本预处理器（PHP）扩展。

要测试 webserver2，请将你的 Web 浏览器指向你机器的 IP 地址（或 localhost 127.0.0.1）以及你所选的 port_number。例如，为了查看我们的 index.html 文件，我们按如下方式设置 URL：

```
192.168.0.6:8083
```

你的 index.html 中定义的任何内容现在都会出现在你的 Web 浏览器中。

当你通过 webserver2 提供 index.html 服务完成后，可以使用 kill 命令停止它，例如：

```
$ sudo kill -9 13325
```

其中
13325 是 webserver2 进程的 PID，如 ps -C webserver2 命令所示。
在继续下一节之前，你应该杀死 webserver2 守护进程。

## 18.5.2.2 webserver 示例程序逻辑模型

参照本书网站上第 W21 章第 3–13 节中所示的各种守护进程程序的基本设计和实现，我们的示例 webserver2 守护进程所包含的系统调用和程序结构与经典的 Linux 守护进程模型非常相似。关于“旧式”Linux 守护进程模型的基本描述，请参阅图 W21.3。

### 练习 18.17

在程序结构的总体层面，webserver2.c 程序的代码与图 W21.3 所示内容之间有哪些差异？

我们的 webserver2 代码与图 W21.3 模型之间的主要差异之一在于程序健壮性的维护。这意味着在该图所示的 11 个步骤中的许多步骤都要进行错误检查和处理，以及系统日志记录。

一个特别的差异是，在 webserver2 中没有将 umask 设置为 0。为什么？

如前所述，我们的示例 webserver2 守护进程与该模型的一个显著例外是，有一个单独的模块负责将所有消息日志（包括错误）记录到 systemd 日志中。因此，例如，每当传入的 Web 服务器请求产生异常时，这些错误都会通过 sd_print_journal 系统调用记录到 systemd 日志中。此外，Web 页面请求和发送也会被记录到 systemd 日志中，从而允许系统管理员将 webserver2 作为服务来监控其运行，并通过超文本传输协议（HTTP）的 GET 和 POST 以及打印到日志中的错误消息来检查可能的入侵警报。

我们在本章末尾提出了一个问题，让你将本书网站上第 W21 章第 3–13 节中创建并在图 W21.3 中总结的系统调用与示例 webserver2 的系统调用进行比较。

## 18.5.2.3 在 webserver2 中使用 Journal 应用程序编程接口（API）

在本小节中，我们将展示 systemd 日志为日志记录提供的原生 API 系统调用。我们还将说明这些原生 API 系统调用在 webserver2 示例程序中的使用。

以下示例代码片段展示了如何使用日志的日志记录 API 调用 sd_journal_print：

```
#include <systemd/sd-journal.h>

int main(int argc, char *argv[]) {
    sd_journal_print(LOG_NOTICE, "systemd rocks!");
    return 0;
}
```

如前所述，该程序必须在 Linux Mint 系统上使用以下编译器指令进行编译。另请注意，还必须先在 Linux Mint 系统上安装 libsystemd-dev 软件包（最便捷的方式是使用软件管理器）。

```
`pkg-config --cflags --libs libsystemd`
```

日志的原生日志记录 API 提供了具有特定结构的日志消息，可从感兴趣的程序（也许是你自己编写并希望在日志中监控这些特定结构的程序）发送到日志中。这些具有特定结构的日志数据可以通过 journalctl 命令进行搜索，并且可供其他辅助程序使用。系统管理员会使用 systemd 日志、辅助程序以及其他入侵检测技术来维护系统安全。附带特定结构数据的日志记录将允许系统管理员在人类可读的日志消息文本之外进一步追踪问题。下面是一个使用系统调用 sd_journal_send() 实现此目的的基本示例：

```
#include <systemd/sd-journal.h>
#include <unistd.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    sd_journal_send("MESSAGE=Hello World!",
                    "MESSAGE_ID=52fb62f99e2c49d89cfbf9d6de5e3555",
                    "PRIORITY=5",
                    "HOME=%s", getenv("HOME"),
                    "TERM=%s", getenv("TERM"),
                    "PAGE_SIZE=%li", sysconf(_SC_PAGESIZE),
                    "N_CPUS=%li", sysconf(_SC_NPROCESSORS_ONLN),
                    NULL);
    return 0;
}
```

上述程序将向日志写入一条日志消息，并附带六个额外的元数据结构化字段。我们使用 sd_journal_send() 来实现这一点，它与 sd_journal_print() 类似，但接受一个以 NULL 结尾的格式字符串列表，每个格式字符串后跟其参数。格式字符串必须包含字段名以及值之前的“=”。

结构化消息包含七个字段。前三个是众所周知的字段：

-   MESSAGE= 是结构化消息中实际人类可读的消息部分。
-   PRIORITY= 是格式化为整数字符串的数字消息优先级值。
-   MESSAGE_ID= 是一个 128 位 ID，用于标识我们的特定消息调用，格式为十六进制字符串。

有关当前所有公认字段的完整列表，请参阅 systemd.journal-fields 的手册页。

在 webserver2 示例中，我们在日志记录模块中使用以下代码结构来向日志打印日志记录信息。各种错误情况，以及最重要的是对守护进程的请求/发送（通过 case 条件 LOG），都以这种方式记录到日志中。

```
switch (type) {
    case ERROR: sd_journal_print(LOG_NOTICE, “ERROR: %s:%s Errno=%d exiting pid=%d”,
                s1, s2, errno, getpid());
        break;
    case FORBIDDEN:
        (void)write(socket_fd, “HTTP/1.1 403 Forbidden\nContent-Length:
        185\nConnection: close\nContent-Type: text/html\n\n<html><head>\n<title>403
        Forbidden</title>\n</head><body>\n<h1>Forbidden</h1>\nThe requested URL,
        file type or operation is not allowed on this simple static file webserver.\
        n</body></html>\n”,271);
        sd_journal_print(LOG_NOTICE, “FORBIDDEN: %s:%s”,s1, s2);
        break;
    case NOTFOUND:
        (void)write(socket_fd, “HTTP/1.1 404 Not Found\nContent-Length:
        136\nConnection: Close\nContent-Type: text/html\n\n<html><head>\n<title>404
        Not Found</title>\n</head><body>\n<h1>Not Found</h1>\n
        The requested URL was not found on this server.\n</body></html>\n”,224);
        /*(void)sprintf(logbuffer,”NOT FOUND: %s:%s”, s1, s2); */
        sd_journal_print(LOG_NOTICE, “NOT FOUND: %s:%s”,s1, s2);
        break;
    case LOG: sd_journal_print(LOG_NOTICE, “INFO: %s:%s:%d”,s1, s2,socket_fd);
        break;
}
if(type == ERROR || type == NOTFOUND || type == FORBIDDEN) exit(3);
}
```

## 18.5.3 将守护进程设为服务：一个简单的三步示例

下面是一个示例，说明如何将第 18.5.2 节中所示的 C 语言系统程序“webserver2”设为 systemd 控制的服务。最简单的方法是为其创建一个单元文件，启动该服务，然后如果希望的话，启用该服务以便在以后每次重新启动时自动启动。

对于一个通用程序，特别是我们的 webserver2 示例，执行此操作所需的步骤如下：

- 步骤 1：使用你喜欢的文本编辑器创建服务单元文件，命名为 **your_name.service**。将该服务单元文件保存到 /etc/systemd/system 目录中。
- 
- 以下是该服务单元文件的内容：
- 
- [Unit]
- Description=一个简单的描述
- After=network.target
