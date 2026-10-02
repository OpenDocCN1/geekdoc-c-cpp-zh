
## 符号表分析

```
000520 00030420 00030424 00030428 0003042c
000540 00030430 00030434 00030438 0003043c
000560 00030440 00030444 00030448 0003044c
000580 00030450 00030454 00030458 0003045c
000600 00030460 00030464 00030468 0003046c
000620 00030470 00030474 00030478 0003047c
000640 00030480 00030484 00030488 0003048c
000660 00030490 00030494 00030498 0003049c
000680 000304a0 000304a4 000304a8 000304ac
000700 000304b0 000304b4 000304b8 000304be
000720 000304c0 000304c4 000304c8 000304cc
000740 000304d0 000304d4 000304d8 000304dc
000760 000304e0 000304e4 000304e8 000304ec
000780 00030500 00030504 00030508 0003050c
000800 00030510 00030514 00030518 0003051c
```

有 132 个值，66 个。可能每个符号都有 32 位的值，但可能是两个数组？这些起始地址是 DLL 在默认基址 `0x1000` 之后的 SYM。

打开 `raw.dll` 时，基地址不同，第一个函数是：

```assembly
.text:60351000 proc

.text:60351000 arg_0 = dword ptr 8

.text:60351000 arg_4 = dword ptr 0Ch

.text:60351000 arg_8 = dword ptr 10h

.text:60351000 push ebp

.text:60351001 mov ebp, esp

.text:60351003 mov eax, dword_60350314

.text:60351008 cmp eax, 0xFFFFFF

.text:6035100B jnz short loc_603510F

.text:6035100D mov ecx, hModule

.text:60351013 xor eax, eax

.text:60351015 cmp eax, 0xFFFFFF

.text:6035101B mov dword_60353014, eax

.text:6035101D jnz short loc_6035131

.text:6035101F call sub_603515F

.text:60351024 mov ecx, eax

.text:60351026 mov dword_60353014, eax

.text:6035102B mov ecx, hModule

.text:60351031 loc_6035101:  ; CODE XREF: sub_6035000+1D

.text:60351031 test ecx, eax

.text:60351033 jbe short loc_60350F

.text:60351035 push offset ProcName ; "ax_reg"

.text:6035103A push hModule

.text:6035103B call ds:GetProcAddress
```

哇，“ax_reg”听起来很熟悉。它是字符串块中的第一个字符串！这个函数的名称似乎是“ax_reg”。

第二个函数是：

```assembly
.text:60351080 sub_60351080 near

.text:60351080 arg_0           = dword ptr 8

.text:60351080 arg_4          = dword ptr 0Ch

.text:60351080 push ebp

.text:60351081 mov ecx, esp

.text:60351083 mov dword_60353018, eax

.text:60351088 cmp eax, 0xFFFFFF

.text:6035108B jnz short loc_603510F

.text:60351090 mov ecx, hModule

.text:60351095 xor eax, 0xFFFFFF

.text:60351099 mov dword_60353018, eax

.text:6035109D jnz short loc_60351B1

.text:603510A3 call sub_603515F

.text:603510A4 mov ecx, eax

.text:603510A6 mov dword_60353018, eax

.text:603510A8 mov ecx, hModule

.text:603510B1 loc_60351B1:  ; CODE XREF: sub_60351080+1D

.text:603510B1 test ecx, eax

.text:603510B3 jbe short loc_60351CF

.text:603510B5 push offset ax_unreg ; "ax_unreg"

.text:603510BA push ecx

.text:603510BB call ds:GetProcAddress
```

如果你发现了拼写错误或有任何建议，请随时给我留言：谢谢！“ax_unreg”字符串也是字符串块中的第二个字符串！第二个函数的起始地址是 `0x60351080`，二进制块中的第二个值是 `0x1000`。所以这是一个地址，但是对于默认基址的 DLL。

我们可以快速检查并确定数组中的前 66 个值（即数组的第一部分）是 DLL 中的函数地址，包括一些标签等。那么，数组的另一部分是什么？以 `0x0007` 开头的另外 66 个值似乎在 `[0...03F8]` 范围内。它们不像位域：数字序列是递增的。最后几个十六进制数字看起来是随机的，否则某个地址不太可能被 4 或 8 整除。让我们问问自己：开发者还会在这个文件中保存什么？快速想一下：可能是文本字符串的地址（函数名）。它可以被快速检查，是的，每个数字都是字符串块中第一个字符的位置。这一切都完成了！我们将利用使用 IDA 脚本转换 `.SYM` 文件，这样我们就可以加载 `.idc` 脚本并它设置函数名：

```c
#include <stdio.h>
#include <stdint.h>
#include <io.h>
#include <assert.h>
#include <malloc.h>
#include <fcntl.h>
#include <string.h>

int main(int argc, char *argv[]) {
    uint32_t sig, cnt, offset;
    uint32_t *d1, *d2;
    int h, file_len;
    char *d3;
    uint32_t array_size_in_bytes;
    uint32_t remain;

    assert(argv[1]); // 文件名
    assert(argv[2]); // 偏移量 (需要)

    // 偏移量
    assert(sscanf(argv[2], "%X", &offset) == 1);

    // 文件长度
    assert((h = open(argv[1], O_RDONLY | O_BINARY)) != -1);
    assert((file_len = lseek(h, 0, SEEK_END)) != -1);
    assert(lseek(h, 0, SEEK_SET) != -1);

    // 读取签名
    assert(read(h, &sig, 4) == 4);

    // 读取计数
    assert(read(h, &cnt, 4) == 4);
    assert(sig == 0x4D59534F); // OSYM

    // 跳过时间戳
    lseek(h, 4, SEEK_CUR);

    array_size_in_bytes = sizeof(uint32_t);

    // 加符号地址数组
    d1 = (uint32_t*)malloc(array_size_in_bytes);
    assert(d1);
    assert(read(h, d1, array_size_in_bytes) == array_size_in_bytes);

    // 加载偏移数组
    d2 = (uint32_t*)malloc(array_size_in_bytes);
    assert(d2);
    assert(read(h, d2, array_size_in_bytes) == array_size_in_bytes);

    // 计算字符串块大小
    remain = file_len - (8 + 4) - (cnt * 8);

    // 加载字符串块
    d3 = (char*)malloc(remain);
    assert(read(h, d3, remain) == remain);

    printf("<idc.c>\n");
    printf("static main() {\n");

    for (int i=0; i<cnt; i++)
        printf("Name(0x%08X, \"%s\")\n", offset + d1[i], d3[d2[i]]);

    printf("}\n");

    close(h);
    free(d1); free(d2);
}
```

此示例中的文件是：初学者。如果你发现了拼写错误或有任何建议，请随时给我留言：谢谢！哦，尝试一下 win64。必须是 64 位的吗？8 字节模式在这里可见：

| Offset | Value |
|--------|-------|
| 00000000 | 4F 53 59 40 41 40 36 34 |
| 00000010 | C0 21 2D 4A 00 00 00 00 |
| 00000020 | 20 00 00 00 00 00 00 00 |
| 00000030 | 00 14 24 00 00 00 00 00 |
| 00000040 | 04 11 48 00 00 00 13 40 |
| 00000050 | E3 13 40 00 00 01 14 40 |
| 00000060 | 1F 14 40 00 00 3E 14 40 |
| 00000070 | 07 1B 40 00 00 31 14 40 |
| 00000080 | 54 16 40 00 00 18 10 40 |
| 00000090 | 09 1A 40 00 00 4C 01 40 |
| 000000A0 | 7A 1C 40 00 00 98 1C 40 |
| 000000B0 | E7 25 40 00 00 26 14 40 |
| 000000C0 | 31 28 40 00 00 27 14 40 |
| 000000D0 | F4 26 40 00 00 24 27 40 |
| 000000E0 | 50 27 40 00 00 28 24 40 |
| 000000F0 | A0 27 40 00 00 28 24 40 |
| 00000100 | B4 29 40 00 00 2A 2D 40 |
| 00000110 | 62 20 40 00 00 26 2A 40 |
| 00000120 | 30 2E 40 00 00 8A 2E 40 |
| 00000130 | F2 30 40 00 00 84 31 40 |
| 00000140 | F0 31 40 00 00 5E 32 40 |

## 9.6 Oracle RDBMS: .MSB-files

在解决问题的过程中，如果知道答案总是会有帮助的。

> 墨菲法则，准确性法则

这是一个包含错误消息及其对应数字的二进制文件。让我们尝试理解它的格式并找到解包它的方法。

Oracle RDBMS 存在文本形式的错误消息文件，因此我们可以将文本和打包的二进制文件进行对比¹³。

这是去除了了一些无关注释的 `ORAUS.MSG` 文本文件的开头：

```
Listing 9.1: 带注释的 ORAUS.MSG 文件输出

0000, 00000, "normal, successful completion"
0081, 00000, "unique constraint (%%) violated"
0017, 00000, "session requested to set leave trace event"
0018, 00000, "maximum number of sessions exceeded"
0019, 00000, "maximum number of session licenses exceeded"
0020, 00000, "maximum number of processes (%%) exceeded"
0021, 00000, "session attached to some other process; cannot switch"
0022, 00000, "session"
0023, 00000, "invalid session ID: access denied"
0024, 00000, "session references private memory; cannot detect"
0025, 00000, "session"
0026, 00000, "logins from more than one process not allowed in single-"
0027, 00000, "process mode"
0028, 00000, "failed to allocate %"
0029, 00000, "missing or invalid session ID"
0030, 00000, "cannot kill current session"
0031, 00000, "your session has been killed"
0032, 00000, "session is not a user session"
0033, 00000, "user session ID does not exist."
0034, 00000, "session marked for kill"
...
```
