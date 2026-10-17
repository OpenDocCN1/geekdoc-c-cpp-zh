
#include <curses.h>

int tty_break() {

    initscr();

    cbreak();

    return 0;

}

int tty_getchar() {

    return getch();

}

int tty_fix() {

    endwin();

    return 0;

}

以下是“经典” (V7, BSD) UNIX 代码：

```c
#include <stdio.h>
#include <sgtyb.h>

static struct sgtyb savemodes;
static int havemodes = 0;

int tty_break() {
    struct sgtyb modmodes;
    if (ioctl(fileno(stdin), TIOCGETP, &savemodes) < 0) {
        return -1;
    }
    havemodes = 1;
    modmodes = savemodes;
    modmodes.sg_flags |= CBREAK;
    return ioctl(fileno(stdin), TIOCSETN, &modmodes);
}
```

```c
int tty_getchar() {
    return getchar();
}
```

```c
int tty_fix() {
    if (!havemodes)
        return 0;
    return ioctl(fileno(stdin), TIOCSETN, &savemodes);
}
```

System V UNIX 的代码类似：

```c
#include <stdio.h>
#include <termio.h>

static struct termio savemodes;
static int havemodes = 0;
```

```c
int tty_break() {
    struct termio modmodes;
    if (ioctl(fileno(stdin), TCGETA, &savemodes) < 0)
        return -1;
    havemodes = 1;
    modmodes = savemodes;
    modmodes.c_lflag &= -ICANON;
    modmodes.c_cc[VMIN] = 1;
    modmodes.c_cc[VTIME] = 0;
    return ioctl(fileno(stdin), TCSETAW, &modmodes);
}
```

```c
int tty_getchar() {
    return getchar();
}
```

```c
int tty_fix() {
    if (!havemodes)
        return 0;
    return ioctl(fileno(stdin), TCSETAW, &savemodes);
}
```

最后，这里是 MS-DOS 的实现：

```c
int tty_break() { return 0; }

int tty_getchar() {
    return getche();
}

int tty_fix() { return 0; }
```

关闭回显（echo）留给读者自行练习。关于终端（键盘和屏幕）I/O 编程的详细信息，请参阅 FAQ 列表、书籍或特定您操作系统的文档集。（注意，可能还有更多细节需要处理，例如要禁用的特殊字符以及更多需要切换的模式位，比文中提到的多。）
另见问题 19.2。

参考文献：PCS $10 pp. 128–9, $10.1 pp. 130–1
POSIX $7

### 问题：我如何知道是否有字符可读（如果有的话，有多少个）？或者，我如何进行一个在没有字符可用时不会阻塞的读取？

**答案：** 这些也完全取决于操作系统。`curses` 的某些版本有一个 `nodelay` 函数。根据你的系统，你可能还可以使用“非阻塞 I/O”，例如名为 `select` 或 `poll` 的系统调用、`FIONREAD` ioctl、`c_cc[TIME]`、`kbhit`、`rdchk` 或通过 `fcntl` 使用 `O_NDELAY` 选项。你也可以尝试使用 `alarm` 让读取在一定间隔后超时（在 UNIX 下查看 `alarm`、`signal` 和 `setimer`）。
如果你正尝试从多个源读取输入，你将需要使用某种 `select` 调用，因为忙等待循环在多任务系统中效率极低。
另见问题 19.1。

## 19.3

### 问题：我如何显示一个原地更新的百分比指示或显示进度条？

**答案：** 这些简单操作，至少可以做到。打印字符 `\r` 通常会给你一个回车而不换行，这样你可以覆盖当前行。字符 `\b` 是退格键，通常会将光标位置向左移动。使用这些字符，你可以打印百分比指示：

```c
for(i = 0; i < lotsa; i++) {
    printf("\r%3d%%", (int)(100L * i / lotsa));
    fflush(stdout);
    do_work();
}
printf("done.\n");
```

或者进度条：

```c
printf("working: ");
for(i = 0; i < lotsa; i++) {
    printf("%c", "|");
    fflush(stdout);
    do_work();
}
printf("\ndone.\n");
```

另见问题 12.4。

参考文献：ANSI $2.2
ISO $5.2

## 19.4

### 问题：我如何清屏？我如何打印反色内容？我如何将光标移动到特定的 x, y 位置？

**答案：** 这些取决于你使用的终端类型（或显示器）。你将需要使用 `termcap`、`terminfo` 或 `curses` 或某些特定系统的程序来执行这些操作。
MS-DOS 库通常有名为 `gotoxy` 和 `lscr` 的函数；你也可以使用 `ANSI.SYS` 驱动或低级中断。在 `termcap` 或 `terminfo` 下，使用 `getstr` 来检索如 `cl`、`sc` 和 `em` 等字符串，用于清屏、反色模式和光标移动；
某些终端还需要注意“特性”。我们知道旧终端可能不支持所需的特性。
对于清屏，一种半可移植方案是打印分页字符 `\f`，这将导致某些显示清屏。更好的移植性是打印足够的换行。作为最后手段，你可以使用 `system`（问题 19.27）调用操作系统的清屏命令。

参考文献：PCS $5.1.4 pp. 54–60, $5.1.5 pp. 60–2

+ Strange, Programming with curses
Strange, Mui, and O’Reilly, termcap & terminfo

![](img/2b27505702f89a0fc85dc6e5851a2984_348_0.png)

### 问题：我如何如何方向键？功能键呢？

**答案：** `Terminfo`、某些版本的 `termcap` 以及某些版本的 `curses` 支持这些非 ASCII 键。通常，特殊键有一个多字符序列（通常以 ESC `\033` 开头）；解析这些序列可能很复杂。如果调用 `curses` 库将为你完成解析。
参考文献：PCS $5.1.4 pp. 56–7

## 其他 I/O

### 问题：我如何读取鼠标？

**答案：** 请咨询你的系统。在 MS-DOS、Macintosh 以及其他所有系统中，鼠标的处理完全不同。
参考文献：PCS $5.5 pp. 78–80

### 问题：我如何进行串口（comm）端口 I/O？

**答案：** 这取决于系统。在 UNIX 下，你通常打开、读取和写入 `/dev` 中的设备文件，并使用终端驱动调整其特性。（另见问题 19.1 和 19.2。）在 MS-DOS 下，你可以使用预定义的 `stdaux`、如 `COM1` 的特殊文件、一些原始中断，或者（如果你需要高性能）任何数量的中断驱动串口 I/O。
参考文献：PCS $5.3 pp. 72–4

## 问题

### 问题：我如何发送转义序列来控制终端或其他设备？

**答案：** 如果你能弄清楚如何向设备发送字符（见问题 19.8），发送转义序列就足够简单。在 ASCII 中，ESC 代码是 033（十进制 27），所以像这样的代码

```c
printf(ofp, "\033[J");
```

发送序列 `[ J`。某些程序员喜欢像这样参数化 ESC 代码：

```c
#define ESC 033
```

```c
printf(ofp, "%c[J", ESC);
```

### 问题：我如何做图形？

**答案：** 曾经，UNIX 有一套非常好的设备无关绘图程序，描述在 `plot(3)` 和 `plot(5)` 中，但它们很大程度上被废弃了。

如果你是为 MS-DOS 编程，你可能想使用符合 VESA 或 BGI 标准的库。

如果你试图与特定的绘图仪通信，让它绘图通常是发送适当的转义序列的问题；另见问题 19.9。供应商可能会提供一个 C 可调用的库，或者你可以在互联网上找到一个。

如果你是为特定的窗口系统（Macintosh、X Windows、Microsoft Windows）编程，你将使用其设施；请查看相关文档或新闻组或 FAQ 列表。

参考文献：PCS $5.4 pp.75–7

## 文件与目录

## 19.11

### 问题：我如何检查文件是否存在？如果请求的输入文件缺失，我想警告用户。

**答案：** 要可靠且可移植地做出这种判断其实出乎意料地困难。在你进行测试和尝试打开文件之间，如果文件被创建或删除（例如通过某个进程），那么你所做的任何测试都会失效。三种可能的例程是 `stat`、`access` 和 `fopen`。（要用 `fopen` 进行近似的存在性测试，只需打开读取并立即关闭。）在这些方法中，只有 `fopen` 是可移植的，如果程序使用 UNIX，则必须小心使用 `access`。与其尝试预测如打开文件等操作是否会成功，往往不如尝试执行它，检查返回值，如果失败则报错报错。（显然，如果你正尝试避免覆盖现有文件，这种方法不起作用，除非你使用了诸如 `O_EXCL` 这样的选项，它可以实现你想要的功能。）

参考文献：PCS §12 pp. 189, 213 POSIX §5.3.1, §5.6.2, §5.6.3

## 19.12

### 问题：我如何在读取文件之前知道“文件大小”？

**答案：** 如果“文件大小”是指你在 C 中能够从文件中读取的字符数（或由之前的程序写入文件的字符数），那么要准确确定这个数字是困难或不可能的（除非读取整个文件）。在 UNIX 下，`stat` 调用（特别是结构体中的 `st_size` 字段）将给你一个准确的答案。其他几个系统提供了类 UNIX 的 `stat` 调用，但除非有进程正在写入该文件，否则文本文件报告的大小可能是近似的（由于换行符表示不同；见问题 12.40）。你可以打开文件并使用 `fstat`，或者使用 `fseek` 跳到文件末尾并使用 `ftell`，但这些方法往往存在相同的问题：`fstat` 不可移植，且通常提供的信息与 `stat` 相同；`ftell` 除了二进制文件外，不保证能返回字节计数。由于某些系统提供了 `filesize` 或 `filelength`，但这些并不是可移植的。

你确定必须提前确定文件大小吗？由于 C 程序确定文件大小最准确的方法是打开并读取文件，也许你可以重新安排代码，在读取时获取大小。（通常情况下，如果读取的字符数与之前的预期不符，你的程序应该优雅地处理，因为任何预先确的大小可能是近似的。）见问题 7.29 和 20.2。

参考文献：ANSI §4.9.9.4 ISO §7.9.9.4 H&S §15.5.1 pp. 352–3 PCS §12 p. 213 POSIX §5.6.2

## 19.13

### 问题：如何在不完全清除或重写文件的情况下缩小文件？

**答案：** BSD 系统提供了 `ftrunc`，其他几个系统提供了 `fsize`，少数系统可能提供（可能是未记录的）`fcntl` 选项 `F_FREESP`。在 MS-DOS 下，你有时可以使用 `write(fd, "", 0)`。然而，没有可移植的解决方案或删除开头块的方法。见问题 19.14。

## 19.14

### 问题：我如何在文件的中间插入或删除一行（或一条记录）？

**答案：** 通常情况下，没有方法可以做到这一点。通常的解决方案是直接重写文件。如果你的操作系统提供非顺序的、面向记录的文件，它可能具有插入/删除操作，但 C 并没有提供特殊支持。

当你发现需要向现有文件插入数据时，这里有一些你可以尝试的替代方案：
- 重新排列数据文件，以便可以在末尾追加新信息。
- 将信息放在第二个文件中。
- 在第一次写入文件时留出一些空白空间（例如 80 个空格的行或像 `000000000` 这样的字段），稍后用最终信息覆盖它（见问题 12.30）。

与其删除记录，你可能考虑只将它们标记为已删除。（顺便提一下，头文件指令中提到的反斜杠不是字符串字量，所以你可能不需要担心那里的反斜杠。）

## 19.15

### 问题：如何删除文件？

**答案：** 在 UNIX 下，使用 `unlink` 调用删除文件。在其他系统中，没有等效函数。

## 19.16

### 问题：如何重命名文件？

**答案：** 在 UNIX 下，`rename` 调用可以移动文件。在其他系统中，你可能必须复制文件然后删除原始文件。

## 19.17

### 问题：如何更改文件的权限？

**答案：** 在 UNIX 下，可以使用 `chmod` 调用。在其他系统中，可能没有等效操作。

## 19.18

### 问题：我收到一个错误：“打开的文件过多（Too many open files）”。我该如何增加允许的打开文件数量？

**答案：** 打开文件数量至少受到两个资源限制：操作系统中可用的低级“文件描述符”或“文件句柄”的数量，以及 stdio 库中可用的 `FILE` 结构数量。两者都必须足够。在 MS-DOS 系统下，你可以通过 CONFIG.SYS 中的某行来控制操作系统文件句柄的数量。某些编译器带有增加 `FILE` 结构数量的说明（可能还有两个源文件）。

## 19.19

### 问题：我如何发现磁盘上有多少可用空间？

**答案：** 没有可移植的方法。在某些版本的 UNIX 下，你可以调用 `stat`。在 MS-DOS 下，使用中断 0x21 子功能 0x36，或者使用诸如 `diskfree` 的函数。另一种可能性是使用管道（见问题 19.30）来调用并读取“磁盘空闲”命令的输出（例如 UNIX 上的 `df`）。注意，磁盘上显然可用的可用空间可能与你能存储的最大文件大小不匹配。）

## 19.20

### 问题：我如何在 C 程序中读取目录？

**答案：** 查看你是否可以使用 `opendir` 和 `readdir` 函数，这些函数是 POSIX 标准的一部分，在大多数 UNIX 变体中可用。MS-DOS、VMS 和其他系统也有实现。（MS-DOS 也有 `FINDFIRST` 和 `FINDNEXT` 例程，本质上相同。）`readdir` 函数只返回文件名；如果你需要关于文件的更多信息，请调用 `stat`。要将文件名与某些通配符模式匹配，见问题 13.7。

这是一个列出当前目录下文件的简单示例：

```c
#include <stdio.h>
#include <sys/types.h>
#include <dirent.h>

main() {
    struct dirent *dp;
    DIR *dfd = opendir(".");
    if(dfd != NULL) {
        while ((dp = readdir(dp)) != NULL) {
            printf("%s\n", dp->d_name);
        }
        closedir(dfd);
    }
    return 0;
}
```
