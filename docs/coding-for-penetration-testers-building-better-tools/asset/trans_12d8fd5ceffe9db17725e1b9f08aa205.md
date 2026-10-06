
如果我们愿意，通过编辑文件来修正这一点非常简单。为了让实际问题的运行得更好一点，我们需要在 `nmap-services-probes` 中添加一个条目。我们可以判断响应来自 `RPCCheck` 探测器，因此我们需要从该行的开始开始查找。如果我们在该行中搜索 `RPCCheck`，我们会在第 7694 行之后找到（它），那里就是该部分的开始，如图 7.3 所示。

![](img/42f332b2adf7dab7e681e5d6cdd2074c_285_0.png)

# 图 7.3 nmap-probes 中的 RPC 探测器。

我们将在这一部分添加此行，以便我们的服务能够被更好地识别。但在这里，我们将提取一段打印指纹并用它来组合成该行。匹配行简单如下：

```
match                               hp-rpc                m\x01\x0\
(r\x5f\x1d\x13\x03\x00\x00\x00\x02\x01\x86| p/Unknown Service
```

该文件中的 `match` 语句使用 Perl 表达式（正则）作为语法。由于我们以 `match` 开头，接着是服务名（我们设置为 `hp-rpc`），然后是匹配字符串、产品名称（我们称之为 `Unknown`）。全部就是这些。现在我们保存文件并再次运行我们的服务扫描（`nmap -sV 10.0.0.51`）来查看结果。这次我们为端口返回了一组不同的信息：

| 端口 | 状态 | 版本 |
| :--- | :--- | :--- |
| 80/tcp | open | http/0.1 (PhotoSmart/Deskjet) |
| 139/tcp | open | netbios-ssn |
| 9100/tcp | open | jetdirect |
| 9101/tcp | open | jetdirect |
| 9102/tcp | open | jetdirect |
| 9110/tcp | open | hp-rpc |
| 9220/tcp | open | hp-gsg |
| 9290/tcp | open | hp-gsg 128.0.4 peripheral gateway |

MAC 地址: 00:15:60:D6:7A (Hewlett Packard)
服务信息: printer (Generic Scan)

根据服务指纹和所使用的探测器，我们可能需要进行微调以获得正确的匹配行。我们希望足够具体，以至于不会包含具有相似指纹的服务，同时包含我们拥有的所有正确信息。在 `match` 行上还可以使用许多其他字段，所有这些字段都包含在 Nmap 文档 [1] 中。

## NSE

NSE (脚本引擎) 本质上等同于一个 Lua 解释器，其本质与我们在本书中讨论的任何其他解释器相似。此外，NSE 脚本需要一些额外的参数，以便 Nmap 能够正确解释它们。让我们先谈谈 Lua，然后回到我们需要如何格式化文件以使其满意的细节。

Lua 用于许多不同应用的有趣之处，例如众所名的《魔兽世界》，以及我们最喜欢的扫描工具 Nmap。我们不会对其进行深入探讨，因为它对本书来说有一个非常具体的用途，即为 NSE 编写脚本。

对于我们可能感兴趣进一步研究 Lua 的人来说，大量的资源可用。关于这个主题已经写了许多书籍，但一个好的起点是在线文档，特别是《Lua 5.1 参考手册》，可以在 http://www.lua.org/docs.html 免费获取。为了参考官方 Nmap 文档的启示，让我们来看一个非常简单的 NSE 脚本 `finger.nse`。此脚本的作用完全如其名：从目标主机上的 `finger` 守护进程检索信息。该脚本的原始源代码可以在 http://nmap.org/svn/scripts/finger.nse 找到。

```
尝试使用 finger 服务检索用户名列表。
author = "Eddie Bell"
license = "Same as Nmap--See http://nmap.org/book/man.html"
categories = {"default", "discovery", "safe"}

-- @output
-- PORT STATE SERVICE
-- 79/tcp open finger
-- finger:
-- Welcome to Linux version 2.6.31.12-0.2-default at linux-pb94.site!
-- 01:14am 18:54, 4 users, load average: 0.14, 0.08, 0.01
-- | Name Tty Idle Login Time Where
-- | *:0 - Wed 06:19 console
-- | pts/1 18:54 Wed 06:20
-- | pts/0 Thu 00:41
-- | pts/4 Thu 01:06
require "comm"
require "shortport"
```
portrule = shortport.port_or_service(79, "finger")
action = function(host, port)
  local try = nmap.new_try()
  return try(comm.exchange(host, port, "\r\n")
  {lines=100, proto=port, timeout=5000})
end
```

脚本从开头到两行之前都是内部文档和元数据。这些行提供了描述、描述性属性以及脚本用法。

两个 `require` 行为脚本引入了库，分别用于通信和构建短端口规则。我们可以在 Nmap 文档中找到可使用的 NSE 库的完整列表。

然后我们设置了检测目标服务的行。`portrule` 行将查找我们指定的端口 79 或名为 `finger` 的服务。假设我们匹配服务的条件满足，我们将执行 `action` 部分的代码。

在这里，我们使用 `try` 设置了错误处理，以便处理任何错误。然后我们使用 `comm.exchange` 打开连接并发送回车行。如果连接成功，我们等待 100 行数据，或者超时 5 秒。

## 构建 Nmap 文件

Lua 不是我们本书到目前为止讨论过的语言。它被用于许多不同应用的有趣之处，例如众所名的《魔兽世界》，以及我们最喜欢的扫描工具 Nmap。我们在这里不会对其进行深入探讨，因为它对本书来说有一个非常具体的用途，即为 NSE 编写脚本。然而，在我们探索简单的 NSE 脚本时，我们将回顾一些基础知识。

## Note

## NASL

好的，让我们直接进入并编写一些 NASL 脚本。NASL 通常与 C 和 Perl 相似，所以如果你熟悉其中任何一种，就应该没问题。如果不是，请回去复习第3 章《Perl 简介》，查看一些 Perl 的讨论和示例，然后回到这里。好的，那么进入池中：

```
socket = open_sock_tcp(21);
if (! socket) exit(0);
```
