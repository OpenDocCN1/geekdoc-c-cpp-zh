
命令行参数。

-   我们可能想要同时搜索多种文件类型，例如 PDF、DOC 和 XLS。我们应该能够通过额外的参数和稍多的循环来处理这些文件类型。
-   目前我们对 `exiftool` 的使用非常有限。然而，我们可以扩展 `if` 语句中的正则表达式，以包含更多 `exiftool` 可以处理的文件类型（实际上类型非常多）。
-   我们目前将下载的文件存放在脚本运行的目录中。如果能将这些文件放在它们自己的目录中，或者 `/tmp` 中就太好了。
-   用于从 Google 列表中提取 URL 有用部分的 `split` 系列非常脆弱，并且会完全跳过某些条目并指向空的 `$url` 变量，这表明解析失败。对这部分进行一些工作可以轻松使其变得更健壮。

这里的示例运行得相当良好，并用于说明我们对各种文件中的元数据可以做一些事情，以及我们可能如何查找它。

# 总结

在渗透测试中，信息收集对我们可能具有巨大的价值。它能使我们收集关于目标人员、系统和环境的信息，并根据这些信息对他们进行攻击。我们收集的信息有许多潜在用途，但我们可能将此类信息的两个主要目的是在社会工程中以及对我们的目标或多个目标进行足迹探测（footprinting）。

我们可以访问的巨大潜在信息源之一是 Google。在 Google 的海量索引中进行搜索可以返回关于人员、设备、文档和文件的特定信息，从中可以获取元数据以及各种其他有趣的信息，前提是我们需要如何正确地进行这些搜索。此外，我们可以将自动化应用于工作中以减轻这项任务。

正如我们在第 3 章《Perl 简介》中所讨论的，Perl 是用于解析文本的精彩工具。我们还可以使用 Perl 自动化网页或应用程序的导航和搜索，在此过程中节省大量工作。我们可以利用各种面向 Web 的 Perl 模块完成很多事情，实现对 Web 的遍历、解析和交互。

元数据（即关于数据的数据）附着在几乎所有文档、文件、视觉媒体和其他用于数字存储信息的结构中，在渗透测试过程中对我们来说可能是无价的。元数据可以提供我们用户名、系统路径、网络服务器名称和路径、被删除的敏感数据以及各种此类有趣的项目。此类信息通常可以通过工具作为字符串或通过类似的搜索工具从文档中轻松恢复。

# 参考文献

- 1. WorldWideWebSize.com, the size of the World Wide Web (The Internet) [Internet]. Available from: http://www.worldwidebsize.com/ (cited 11.12.15).
- 2. Google Hacking Database, GHDB, Google Dorks [Internet]. Available from: https://www.exploit-db.com/google-hacking-database/ (cited 11.12.15).
- 3. Andy Lester, search.cpan.org [Internet]. Available from: http://search.cpan.org/~petdance/ (cited 11.12.15).

> ¹https://www.exploit-db.com/google-hacking-database.
²http://www.googleguide.com/

# 第 9 章

# 漏洞脚本

# 摘要

使用和构建利用的能力是渗透测试区别于漏洞扫描的。本章将介绍使用 Python 从零开始构建一个简单的利用。一旦 Python 迫使应用程序屈服并向我们返回 shell，我们将转向 Ruby，通过将其转换为 Metasploit 模块使其变得可重复且更强大。在探索了二进制利用的世界后，本章将进入 Web 应用测试，并研究如何处理远程文件包含（RFI）漏洞和跨站脚本（XSS）漏洞。本章将介绍如何使用 RFI 漏洞并利用第 5 章《PHP Web 脚本简介》中创建的 shell，从 Web 漏洞进入命令行，并以构建额外的脚本使用 XSS 窃取数据结束。

# 关键词

利用（Exploitation）；利用程序；Python；Web；Ruby；RFI；XSS

# 本章内容

- 使用 Python 构建利用程序
- 创建 Metasploit 利用程序
- 利用 PHP 脚本
- 跨站脚本

# 引言

渗透测试员必须理解如何使用脚本语言构建利用程序，以便在实际语文中有效率应用它们。得益于其网络库和快速原型代码的能力，Python 是构建概念验证（POC）利用程序的流行语言。本章从概述为示例 Linux 二进制文件构建 POC 利用程序的步骤开始。作为数据提交的长字符串将导致此应用程序以可被利用的方式崩溃；因此，本章将检查从第一次崩溃到可工作的利用程序的创建过程，解释如何设置第一次崩溃、使用各种辅助脚本、控制 EIP、添加 shellcode 并获取 shell。接下来，它讨论了如何将 Python 脚本转换为 Ruby 中更灵活的 Metasploit 模块。本章最后详细讨论了使用 PHP 不同风格的 Web 攻击。

现在已经在第 2 章和第 5 章《Python 简介》和《PHP Web 脚本简介》中介绍了 Python 和 PHP，让我们来看看如何将基础渗透测试技能提升到水平。虽然我们将使用的许多利用程序已经为我们构建好了，有时我们希望超越基础。无论是为了包含新的负载还是修复损坏的利用程序，我们都希望理解使用脚本语言构建利用程序的过程，以便在实际环境中有效应用它们。

# 使用 Python 构建利用程序

Python 是构建概念验证（POC）利用程序的流行语言。例如，可以在 exploit-db.com（一个包含渗透测试利用程序的流行在线数据库）上搜索 Python。Python 的网络库和快速原型代码的能力是其作为流行语言的主要原因。在本节中，我们将为示例 Linux 二进制文件构建 POC 利用程序。作为数据提交的长字符串将导致此应用程序以可被利用的方式崩溃；我们将检查从第一次崩溃到可工作的利用程序的创建过程。

# 设置

对于这个练习，我们将使用 Kali Linux。默认情况下，Linux 有若干保护措施，包括地址随机化、不可执行栈和栈金丝（stack canary）。为了让此示例利用工作，我们必须为我们的示例程序禁用这些内容。

首先，我们需要禁用栈随机化。这是一个可以通过 proc 文件系统操作的设置。通过执行命令 `echo 0 >/proc/sys/kernel/randomize_va_space`禁用地址布局随机化。这在重启后不会持续，确保每次都关闭它，或者在 /etc/sysctl.conf 文件中添加行 `kernel.randomize_va_space = 0`。

我们将创建一个漏洞程序。为此，将以下代码复制到名为 vuln.c 的文件中：

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <errno.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <arpa/inet.h>
// 返回 ESP 的值
unsigned long getsesp()
{
    asm ("mov %esp, %eax");
}
// 如果 mystr 很大会导致崩溃的漏洞函数
void crash(char *mystr, int myfd)
{
    char buf[256];
    // 将消息发回客户端
    send(myfd, mystr, strlen(mystr), 0);
    // 执行覆盖 EIP 的内存拷贝
    memcpy(buf, mystr, strlen(mystr));
}
int main()
{
    int fd;
    struct sockaddr_in self;
    char buf[2048];
    // 创建新 socket
    if (fd = socket(AF_INET, SOCK_STREAM, 0)) < 0 )
```
