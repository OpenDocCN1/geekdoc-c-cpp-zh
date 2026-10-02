
## Rnd 函数分析

```assembly
.text:01003940 : _stdcall Rnd(x)

.text:01003940 :Rnd_4 proc near ; CODE XREF:

.text:01003940 :0553 ; StartGame()+61

.text:01003940

.text:01003940 arg_0 : dword ptr 4
```

> ⁴ 本书作者这样做是为了给他的同事们开一个玩笑，希望他们能停止玩游戏。但他们没有。

如果你发现了拼写错误、错误或有任何建议，请随时给我留信：我的邮箱。谢谢！

```assembly
.text:01003940    call ds:imp__rand

.text:01003940    cdq

.text:01003946    idiv [esp+arg_0]

.text:01003947    eax, edx

.text:01003948    mov 4

.text:01003950    retn

.text:0100394D    Rnd@4 endp
```

IDA 是这样命名它的，而它是被扫雷开发者赋予这个名字。

该函数非常简单：

```c
int Rnd(int limit)
{
    return rand() % limit;
}
```

（PDB 文件中没有 "limit"；是我们手动命名了这样的内容）
所以它返回一个从 0 到指定限制的随机值。

`Rnd()` 只从一个地方被调用，即函数 `StartGame()` 中，看起来这正是放置地雷的代码：

```assembly
.text:010036C7    push xBox

.text:010036CD    call Rnd@4 ; Rnd(x)

.text:010036D2    push yBox

.text:010036D8    mov esi, eax

.text:010036DA    inc esi

.text:010036E0    call Rnd@4 ; Rnd(x)

.text:010036E4    mov eax, eax

.text:010036E6    shl esi, 5

.text:010036EB    test rgb[esi], 80

.text:010036EE    jnz loc01003C7

.text:010036F0    shl eax, 5 ; EAX=EAX*32

.text:010036F3    lea eax, rgb[esi+eax]

.text:010036FA    or byte [eax], 80

.text:010036FD    call BombStart

.text:01003703    jnz loc01003C7
```

扫雷允许你设置大小，`x (xBox)` 和 `y (yBox)` 是全局变量。它们被传递给 `Rnd()` 并生成随机坐标。如果 `OR` 指令之前已经放置了地雷，`JNZ` 会跳转到 `0x1003E6`。`BombStart` 是包含地雷总数的全局变量。这是一个循环。数组的宽度是 32（我们可以通过乘以 32 的指令来确认）。

如果你有任何拼写错误、错误或建议，请随时给我留信：我的邮箱。谢谢！

`rgb` 全局数组的大小可以通过数据段中下一个 rgb 标签之间的差异轻松确定。它是 `0x360 (864)`：

| 地址 | 十进制 |
| :--- | :--- |
| 01005340 | 10 10 10 10 10 10 10 10 0F 0F |
| 01005350 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 01005360 | 10 0F 0F 0F 0F 0F 0F 10 0F 0F |
| 01005370 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 01005380 | 10 0F 0F 0F 0F 0F 0F 0F 10 0F 0F |
| 01005390 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 010053A0 | 10 0F 0F 0F 0F 0F 0F 0F 10 0F 0F |
| 010053B0 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 010053C0 | 10 0F 0F 0F 0F 0F 0F 0F 10 0F 0F |
| 010053D0 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 010053E0 | 10 0F 0F 0F 0F 0F 0F 10 0F 0F 0F |
| 010053F0 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 01005410 | 10 0F 0F 0F 0F 0F 0F 10 0F 0F 0F |
| 01005420 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 01005430 | 10 0F 0F 0F 0F 0F 0F 10 0F 0F 0F |
| 01005440 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 01005450 | 10 0F 0F 0F 0F 0F 0F 1F 0F 0F |
| 01005460 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 01005470 | 10 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 01005480 | 10 10 10 10 10 10 10 00 0F 0F |
| 01005490 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 010054A0 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 010054B0 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |
| 010054C0 | 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F |

line #7:
01005420 10[8F]0F 0F[8F]0F 0F 0F 10 0F 0F 0F 0F
01005430 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F
line #8:
01005440 10[8F]0F 0F 0F[8F]0F[8F]10 0F 0F 0F 0F
01005450 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F
line #9:
01005460 10 0F 0F 0F [8F]0F 0F [8F]10 0F 0F 0F 0F
01005470 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F
border:
01005480 10 10 10 10 10 10 10 0F 0F 0F 0F 0F
01005490 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F

现在我们将移除所有边界字节（0x10）以及其之后的内容：

```
0F 0F 0F 0F 0F 0F
0F 0F 0F 0F 0F 0F
0F 0F 0F 0F 0F[8F]0F
0F 0F 0F 0F 0F 0F
0F 0F 0F 0F 0F 0F
0F[8F]0F 0F[8F]0F 0F 0F
[8F]0F 0F[8F]0F 0F 0F 0F
[8F]0F 0F 0F [8F]0F[8F]
0F 0F 0F [8F]0F 0F[8F]
```

是的，这些就是地雷，现在可以清晰地看到并与截图对比了。

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

有趣的是，我们可以直接在 OllyDbg 中修改数组。我们可以通过将所有的 0x8F 字节更改为 0x0F 来移除所有地雷，以下是我们在扫雷游戏中得到的结果：

![](img/4590a0c34d3b5b6ca77b4202d4036d48_1046_0.png)

图 8.8：调试器中已移除了所有地雷

我们还可以将它们全部移动到第一行：

![](img/4590a0c34d3b5b6ca77b4202d4036d48_1046_1.png)

图 8.9：调试器中设置的地雷

嗯，调试器并不方便用于监听（这反恰是我们的目标），所以我们将编写一个小型工具来转导出棋盘的内容：

```c
// Windows XP 扫雷作弊器
// 由 dennis(a)yurichev.com 编写，用于 http://beginners.re/ 书
#include <windows.h>
```

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

1027

```c
#include <assert.h>
#include <stdio.h>

int main(int argc, char * argv[])
{
    int i, j;
    HANDLE h;
    DWORD PID, address, rd;
    BYTE board[27][32];

    if (argc!=3)
    {
        printf("Usage: %s <PID> <address>\n", argv[0]);
        return 0;
    }

    assert(argv[1]!=NULL);
    assert(argv[2]!=NULL);
    assert(sscanf(argv[1], "%d", &PID)==1);
    assert(sscanf(argv[2], "%x", &address)==1);

    h=OpenProcess(PROCESS_VM_OPERATION | PROCESS_VM_READ | PROCESS_VM_WRITE, FALSE, PID);

    if (h==NULL)
    {
        DWORD err=GetLastError();
        printf("OpenProcess error: %08X\n", err);
        return 0;
    }

    if (ReadProcessMemory(h, (LPVOID)address, board, sizeof(board), &rd)!=TRUE)
    {
        printf("ReadProcessMemory failed\n");
        return 0;
    }

    for (i=1; i<26; i++)
    {
        if (board[i][0]==0x10 && board[i][1]==0x10) // 注意：此处原文为 board[i][0] 可能是逻辑逻辑，此处按原文翻译
        // 修正逻辑理解：原文为 if (board[i][0]==0x10 && board[i][1]==0x10) 此处可能有误，但保持原样
        break; // 棋盘结束

        for (j=1; j<31; j++)
        {
            if (board[i][j]==0x10)
                break; // 边界

            if (board[i][j]==0x8F)
                printf("*");
            else
                printf(" ");
        }
    }
```

如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

```c
printf("\n");
CloseHandle(h);
```

只需设置 PID 和数组地址（Windows XP 为 0x1005340），它就会导出。通过 PID 附加进程并读取进程内存。

## 8.4.1 寻找网格

每次运行工具都要手动设置地址很麻烦。已知始终有边界（0x10），我们可以直接在内存中找到它：

```c
// 确定帧地址
process_mem=(BYTE*)malloc(process_size);
assert(process_mem==NULL);
if (ReadProcessMemory(h, (LPVOID)start_addr, process_mem, &id)==TRUE) {
    printf("ReadProcessMemory failed\n");
    return 0;
}

// 用于 9x9 网格
// FIXME: 慢了！
for (i=0; i<process_size; i++) {
    if (memcmp(process_mem+1, "\x10\x10\x10\x10\x10\x10\x10\x10", 32) == 0) {
        // 找到了
        address=start_addr+i;
        break;
    }
}

if (id==0) {
    printf("Can't determine address of frame (and grid)\n");
    return 0;
} else {
```

> 可以在任务管理器查看 PID（查看 -> 选择列）
> 编译后的可执行文件在这里：beginners.re

如果你发现了任何拼写错误、错误或有任何建议，请随时给我写信：我的邮箱。谢谢！

```c
printf("Found frame and grid at %0x\n", address);
```

完整源码：https://beginners.re/current-tree/examples/minesweeper/minesweeper_cheater.c.

## 8.4.2 练习

- 为什么边界字节（哨兵值）0x10 存在数组中？
- 如果它们在扫雷界面不可见，它们的作用是什么？没有它们如何运行？
- 结果还有其他可能的值（用于开启区域、用户标记等）。尝试找到每个值的含义。
- 修改我的工具，使其能够移除所有地雷或在当前运行的扫雷进程中将其设置为固定模式。

## 8.5 破解 Windows 时钟

有时会对同事开个玩笑。看看我们能不能对 Windows 时钟做点什么？我们可以强制时针倒转吗？
首先，当你点击状态栏上的日期/时间时，会执行 `C:\WINDOWS\SYSTEM32\TIMEDATE.CPL`，这是一个通常的可执行文件。
看看它是如何绘制时针的？当我用 Resource Hacker 打开文件（来自 Windows 7）时，有表盘但没有时针：

![](img/4590a0c34d3b5b6ca77b4202d4036d48_1050_0.png)

图 8.10：Resource Hacker

好了，我们知道什么？如何绘制时针？它们都始于圆心，止于边界。因此，我们必须计算圆盘上点的坐标。从中学数学回记得我们需要使用正弦/余弦函数来画圆，或者至少使用平方根。在 `TIMEDATE.CPL` 中一眼并没有这些东西。但多亏了微软调试 PDB 文件，我找到了 `CatalogClock::DrawHand()` 方法，它至少了两次 `Graphics::DrawLine(HDC)`。

这是它的代码：

```assembly
.text:6EB90DC7: private: enum Gdiplus::Status _thiscall
CatalogClock::DrawHand(Gdiplus::graphics *, int, struct ClockHand
Const & class, Gdiplus::Pen *)

.text:6EB90DC7: *DrawHandCatalogClock@@*4430@Gdiplus@@PAV@@Clock@@VPen@@Z proc near

.text:6EB90DC7: XREF; CatalogClock::ClockPoint(HDC)+163

.text:6EB90DC7:CatalogClock::ClockPoint(HDC)+18B

.text:6EB90DC7: var_10 = dword ptr -10h

.text:6EB90DC7: var_7 = dword ptr -C

.text:6EB90DC7: var_6 = dword ptr -8

.text:6EB90DC7: var_4 = dword ptr -4

.text:6EB90DC7: arg_0 = dword ptr 8

.text:6EB90BC7: arg_4=dword ptr 0C

.text:6EB90BC7: arg_8=dword ptr 0h

.text:6EB90BC7: arg_C=dword ptr 4h

.text:6EB90BC7: mov edi, edi

.text:6EB90BC9: push ebx

.text:6EB90BCA: mov esp

.text:6EB90BCC: sub esp

.text:6EB90BCF: push 3C

.text:6EB90BD0: push esi

.text:6EB90BD2: pop ebx

.text:6EB90BD5: idx

.text:6EB90BD8: push 2

.text:6EB90BDE: lea eax, [edx+4)

.text:6EB90BE6: mov [ebp+4], eax

.text:6EB90BF9: call

.text:6EB90BFC: call

.text:6EB90C00SetInterpolationMode(Graphics::Gdiplus::Status=2@diplus::InterpolationMode)

.text:6EB90C01: mov eax, [ebp-7h]

.text:6EB90C04

.text:6EB90C07: mov eax, [esi+70h]

.text:6EB90C0A: mov [ebp-8]
```
