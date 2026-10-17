
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
