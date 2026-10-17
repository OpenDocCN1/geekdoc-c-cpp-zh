
这些标志传递给链接器以移除调试信息并剥离二进制文件。

## 添加 ASCII Art

你的实现可能一团乱糟，但如果它有 ASCII Art，它看起来就是合法的。好吧，我们不是认真的。但出于某种原因，每个安全工具似乎都有 ASCII Art，也许你也应该在你的程序里加上，这是可选的。

## 总结

Go 是编写跨平台植体的极佳语言，比如你在本章中构建的 RAT。创建植体可能是该项目中最困难的部分，因为与专为系统 API 设计的语言（如 C# 和 Windows API）相比，使用 Go 与底层操作系统交互可能具有挑战。此外，由于 Go 构建的是静态编译的二进制文件，植体可能会导致二进制文件较大，这会对分发产生一些限制。

但对于后端服务，没有比它更好的了。本书的作者之一（Tom）与另一位作者（Dan）有一个赌注：如果他以后不再使用 Go 进行后端服务和通用工具开发，他必须支付 10,000 美元。目前还没有迹象显示他会切换（尽管 Elixir 看起来很酷）。使用书中描述的所有技术，你应该有一个坚实的基础来开始构建健壮的框架和工具。

我们希望你喜欢这本书以及参与练习。我们鼓励你继续编写 Go，并利用书中学的技能构建增强或替换你当前任务的小工具。随着经验的积累，开始处理更大的代码库并构建一些棒的项目。要继续提升技能，请查看一些流行的 Go 项目，特别是来自大型组织的项目。观看 GopherCon 等会议的演讲，它们可以引导你学习更高级的主题，并对陷阱和增强编程的方法进行讨论。最重要的是，要开心——如果你构建了什么酷东西，告诉我们！

身份验证，67, 86–88, 239–241

## B
反引号（backticks），19

基础工作区目录，2

Base64 编码，215–216

bcrypt 哈希，235, 237–239

信标（Beacon），121

伯克利包过滤器（Berkeley Packet Filter, BPF），175, 181. 参见 tcpdump

最佳实践
- 编码，19, 49, 66, 185, 195, 329
- 安全，96, 236

bin 目录，2

二进制文件，2

二进制数据处理，213–216

Bing，68–76

bodyType 参数，46

大括号（braces），14

break 语句，14

暴力破解，252–261

缓冲区溢出模糊测试，188–192

缓冲通道（buffered channels），29, 37–39

bufio 包，38, 112–113, 197

build 命令，7

构建约束，7–8

字节切片（byte slices），19

bytes 包，197

## C
C语言，201–212, 290–293

c 转换，213

Caddy 服务器，127

.Call() 方法，273

规范别名（CNAME）记录，109–111

capture() 函数，184

CGO 包，291

通道（channels），16–17

Checker 接口，220–222

密码块链接链（CBC）模式，242

密文，234

明文（cleartext）
- 概述，234
- 密码，150
- 嗅探，178–180

客户端植入体（client implants），323–325, 327–329

Client 结构体，53–54

克隆网站，90–93

Close() 方法，25

关闭端口，22

Cmd，41

CNAME 记录，109–111

Cobalt Strike，118–124, 278

COFF 文件头，282–283

碰撞，234

Command() 函数，41

## commands
- build 命令，7
- 交叉编译，7–8
- go 命令，6–9
- set 命令，3
- 复杂数据类型，10–11
- 并发并发，16–17, 37
- 并发扫描，26–32
- Conn，35–38
- 连接，24–25, 35, 327
- 约束，7–8
- 控制结构，14–16
- 便利函数，46–47, 140
- Copy() 函数，40
- createChunkCRC() 方法，304–305
- CreateRemoteThread() Windows 函数，275–276
- 凭据采集攻击，90–93
- 关键数据块，302
- 交叉编译，7–8
- 跨站脚本，94
- crypto 包，197, 235
- 加密学（cryptography）
  - 概述，234–235
  - 哈希，234–239
- curl，40, 79

## D
数据目录（Data Directory），285–287

数据映射，71–73, 125

数据类型
- 通道，16
- 映射，11
- 原生，10–11
- 切片，11

数据库矿工，161–170

debug 包，197

decoder 函数，300

解码过程，308

解密，234. 参见加密

DefaultServerMux，78–79

defer，49

DELETE 请求，47–48

dep 工具，9

开发环境搭建，1–10

Dial() 方法，24

方言（dialects），132–133

指令（directives），19

Dirty COW，201–204

DNS 客户端，104–117

DNS 代理，124–127

DNS 服务器，117–129

DNS 隧道协议，121

do 循环，15

Docker，90, 118–122, 154–158

文档元数据，69

文档对象模型（DOM），74

域名劫持（domain fronting），98

DOS 头部，281

DWORD，271

## E
echo 服务器，32, 35–37

Empire，121

Encode() 方法，65

decode() 函数，308

encoding 包，197

编码过程，308

加密，234, 242–252

字节序（endianness），299

错误处理，17–18

错误消息，51

异或（XOR），307–312

可执行链接格式（ELF），203

漏洞利用，196–212

导出地址表（EAT），279

## F
字段标签，19–20, 139

文件系统，170–171

文件类型（filetype），73

过滤端口，22

过滤结果，73–76

防火墙，22–23

固定字段标签，140

Flusher，42

fmt 包，25

Foo 结构体，19

for 循环，15

格式化数据，38, 113–114

Frida，278

完全域名（FQDN），104

模糊测试，188–196

## G
g 安全漏洞，41

Get() 函数，46

get() HTTP 函数，227–229

GetLibAddress() 函数，275

GetProcessAddress() Windows 函数，275

GetSchema() 函数，163

GitHub Atom，4–5

290

go build 命令，6–7

Go DNS 包，104

go doc 命令，8

go fmt 命令，9

go get 命令，8–9

Go Playground 环境，10

go run 命令，6

## Go Syntax
- 复杂数据类型，10–11
- 并发，16–17
- 控制结构，14–16
- 数据类型，10–11
- 接口类型，13
- 映射，11
- 模式，12–14
- 指针，12
- 原生数据类型，10–11
- 切片，11
- 结构体类型，12

go vet 命令，9

GOARCH 约束，7–8

GoLand，5–6

golint 命令，9

GOOS 约束，7–8

gopacket 包，174

gopacket/pcap 子包，174–175

GOPATH 环境变量，2–3

goquery 包，69

gorilla/mux 包，82–83, 84, 101

gorilla/websocket 包，96

GOROOT 环境变量，2–3

goroutines，16–17, 26–32

##RPC 框架，316–319

gss 包，138

## H
HandleFunc() 方法，82

handler() 函数，75–76

握手过程，22–23

基于哈希的身份验证，147–150

哈希，234–239

Head() 函数，46

hex 转换，214

进制，198, 281, 297

HMAC（密钥哈希消息认证码）标准，240–241

Holt, Matt，127

主机搜索，55–57

HTTP 客户端
- 概述，46–51
- Bing 爬虫，68–76
- Metasploit 交互，59–68

Shodan 交互，51–59

HTTP 服务器
- 概述，78–90
- 凭据采集攻击，90–93
- 多路复用，98–102
- WebSocket API，93–98
- http.HandleFunc(),78–79

## I
- if 语句，18
- 植入代码，323–325, 327–329
- 导入地址表（IAT），279
- 索引元数据，68–76
- 无限循环，37
- init() 函数，101
- 输入/输出（I/O）任务，32–35
- 流过滤器，73
- 集成开发环境（IDEs），3–6
- interface() 类型，97
- 接口类型，13
- io 包，32, 197
- io.Pipe() 函数，43

- io.ReadCloser，49

- io.Reader，32–35, 46
- ioutil.ReadAll() 函数，49

- io.Writer，32–35

## J
Java，218–220

JavaScript，94–95

JetBrains GoLand，5–6

JSON，19, 50

## K
Kerberos，135

Kernel32.dll，275

密钥哈希消息认证码（HMAC）标准，240–241

键盘记录，93–98

## L
轻线程，16–17

len 字段标签，140

库，2

load() 函数，275

Login() 方法，66

循环，15

Lua 环境，118–122, 154–158

8

Luhn 校验，253–254

## M
MinGW-w4，290

mod 工具，9

MongoDB 数据库，161–170

MsfV2，213

Msg 结构体，106

MSYS2，290

多通道通信，30–32

多路复用，98–102

互斥锁（mutex），129

相互身份验证，248–252

MySQL 数据库，157–158, 160

## N
命名函数，126

原生插件，218–224

negroni 包，83–88

Nessus 漏洞扫描，217

net 包，24–25, 197

Netcat，40–44

net.Conn，35–38

New() 辅助函数，53–54

NewProperties() 函数，72–73

NewRequest() 函数，48

nmap，225

非并发扫描，25–26

NoSQL 数据库，154–156, 160

## O
混淆，307

Office Open XML 文档，69

offset 字段标签，140

偏移值，300

omitempty，62

开放端口，22

OPSEC，329

可选头部，284–285

Oracle，154

os 包，197

os/exec 包，41

## P
包，2, 8–9

包捕获与过滤，175–180

panic() 函数，107, 112

parseTags() 函数，140–142

被动侦察，51, 59

哈希传递身份验证，147–150

# 索引

密码, 146–151, 222–224

PATCH 请求, 47

有效负载, 101, 302–307

pcap, 175

PDF 文件, 69

PE（可执行文件）格式, 279–289

PipeReader, 43

PKCS（公公密钥密码学标准）, 242。参见公钥加密

pkg 目录, 2–3

占位符, 83, 89

Plan 9 操作系统, 216

插件
- Lua, 225–232
- 原生, 218–224
- 插件包, 219

PNG 格式, 296–307

指针, 12

可执行文件 (PE) 格式, 279–289

可移植网络图形 (PNG) 图像, 296–307

端口
- 可用性, 24–25
- 握手过程, 22
- 端口转发, 23, 39–40
- 端口扫描器, 180–185, 222–224
- 扫描, 23–32。参见端口

Post() 函数, 46–47

PostForm() 函数, 47

Postgres 数据库, 156–157, 160–161

PostgreSQL 数据库, 156–157, 160–161

PreProcessImage() 函数, 298

基本型数据类型, 10–11

process() 函数, 72–73

Process Hacker, 278

进程注入, 268–269

Process Monitor, 278

ProcessImage() 方法, 302–303

processselfmem() 函数, 205

项目结构, 52–53, 60

promisc 变量, 177

Protocol Buffers (Protobuf), 316

PsExec, 131

公钥加密, 242, 245。*参见*加密

PUT 请求, 47–48

Python, 197–201

# Q

查询参数, 73–76

# R

竞态条件函数, 206

Rapid7, 60

RATs（远程访问木马）, 315–329

原始转换, 215

RC2, 252–261

ReadString() 函数, 38

侦察, 51, 59

重定向器, 98

引用字段, 138–139

reflect 包, 139

反射, 132, 139

正则表达式 (regex) 值, 163

远程访问木马 (RATs), 315–329

远程过程调用 (RPCs), 59, 64–67, 316

请求/响应周期, 46, 62–64

响应处理, 48–51

Rivest, Ron, 252

RLock, 129

Roundcube, 90

路由器, 79–80, 84–85

Rst 包, 22

# S

盐值, 234

scanner 包, 220, 223

扫描器, 23–32, 180–185, 217, 222–224。参见端口

无模式数据库, 154

元数据抓取, 68–76

Search() 函数, 163
-搜索查询模板, 73–76

节表 (Section Table), 287–289

安全令牌, 133–134

send() 方法, 65

serveFile() 函数, 97

服务器消息块 (SMB), 132–147

服务器多路复用, 78–79

ServerMux, 78–79

SessionList() 方法, 66, 68

set 命令, 3

SHA-256 哈希值, 236–237

shellcode, 203–204, 213–216

Shodan, 51–59

签名验证, 245–248

站点过滤器, 73

切片 (slices), 11, 106, 126, 144–145

SQL 注入模糊测试, 192–196

SQLite 数据库, 328

src 目录, 3

无状态协议, 46

静态文件, 93

Status struct, 50–51

隐写术
- 概述, 295
- PNG 格式, 296–307
- XOR, 307–312

strconv 包, 25

strlen() 函数, 17

strToInt() 方法, 304

结构体 (structs)
- APIInfo struct, 55
- Client Struct, 53–54
- 编码, 135
- Foo struct, 19
- 处理, 142–143
- Msg struct, 106–107
- Status struct, 50–51
- 类型的, 12–13, 19

结构化数据, 50–51

子目录, 2–3

子域名, 107

switch 语句, 143

交换网络, 178

对称算法, 234

对称密钥加密, 242–245。参见加密

SYN Cookie, 180

22

SYN 洪水防护, 180–185

syscall 包, 197

Syscall() 函数, 210

# T

tab 包, 113–114

目标突破, 154

TCP 标志, 180–181

tcpdump, 102, 105, 175–178

传输控制协议 (TCP)
握手过程, 22–23

# U

Ubuntu 虚拟机, 118–120

uint 数据类型, 143–144

uintptr 类型, 266

unicode 包, 197

unmarshal() 函数, 19

反序列化接口, 136–142

unsafe 包, 197

unsafe.Pointer 类型, 266–267

USER 属性, 190

# V

变量命名规范, 89

动词, 47

Vim 编辑器, 3–4

虚拟机 (VMs), 118–120

虚拟内存, 273–274

VirtualAllocEx, 273–274

VirtualFreeEx() 函数, 277–278

VS Code, 5

漏洞模糊器, 188–196

# W (此处略)

# X

XML, 19–20, 69

XOR, 307–312

Black Hat Go 使用字体为 New Baskerville, Futura, Dogma 和 The Sans Mono Condensed。

# 更新

访问 https://nostarch.com/blackhatgo/ 获取更新、勘误和其他信息。

更多来自 NO STARCH PRESS 的实用书籍

# 实战漏洞挖掘

Web 攻击指南

PETER YAWORSKI 著

2019年7月, 264 页，$39.95

ISBN 978-1-59327-861-8

# 恶意软件数据科学

攻击检测与溯源

JOSHUA SAXE 著
HILLARY SANDERS 助

2018年9月, 272 页，$49.95

ISBN 978-1-59327-859-5

# 脚注

## 第 2 章：TCP、扫描器与代理

1. 这是由 Nmap 的创建者 Fyodor 提供的免费服务，但在你进行扫描时，请保持礼貌。请求：“尽量不要过度地猛击服务器。每天扫描几次是可以的，但不要每天扫描 100 次。”

## 第 3 章：HTTP 客户端与工具的远程交互

1. 如需漏洞利用协助和练习，可以考虑下载并运行 Metasploit 虚拟机镜像，其中包含了几个用于训练的待利用漏洞。

## 第 5 章：利用 DNS 漏洞

1. Go 1.9 及更高版本包含一种并发安全的类型 `sync.Map`，可以使用它来简化你的代码。

## 第 9 章：编写和移植漏洞代码

1. 关于此漏洞的更多详细信息，请参参 https://foxvesecurity.com/2015/11/06/what-do-weblogic-websphere-jenkins-jboss-opennms-and-your-application-have-in-common-this-vulnerability/#jboss

## 第 11 章：密码学的实现与攻击

1. 某些工作模式，例如 Galois/计数器模式（GCM），提供了完整性保障。
```
