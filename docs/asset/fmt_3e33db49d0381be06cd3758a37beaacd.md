
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
