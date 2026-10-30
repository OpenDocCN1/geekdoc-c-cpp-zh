
STATUS 即 BSD 状态请求字符。在扩展规范模式（同时设置 IEXTEN 和 ICANON 标志）下，该字符在输入时被识别，并产生 SIGINFO 信号，该信号被发送到前台进程组中的所有进程（参见图 9.7）。此外，如果 NOKERNINFO 标志未设置，则前台进程组的状态信息会显示在终端上。该字符在处理时被丢弃（即不会传递给进程）。

STOP 即停止字符。如果设置了 IXON 标志，该字符在输入时被识别；如果设置了 IXOFF 标志，该字符会自动作为输出生成。当 IXON 置位时，接收到 STOP 字符会停止输出。在这种情况下，STOP 字符在处理时被丢弃（即不会传递给进程）。当输入 START 字符时，停止的输出会重新启动。

当 IXOFF 置位时，终端驱动程序会自动生成 STOP 字符，以防止输入缓冲区溢出。

SUSP 即挂起作业控制字符。如果支持作业控制且设置了 ISIG 标志，该字符在输入时被识别。挂起字符产生 SIGTSTP 信号，该信号被发送到前台进程组中的所有进程（参见图 9.7）。该字符在处理时被丢弃（即不会传递给进程）。

WERASE 即删除单词字符。在扩展规范模式（同时设置 IEXTEN 和 ICANON 标志）下，该字符在输入时被识别，并导致前一个单词被删除。首先，它向后跳过任何空白字符（空格或制表符），然后向后跳过前一个标记，使光标停留在前一个标记第一个字符所在的位置。通常，前一个标记在遇到空白字符时结束。但是，我们可以通过设置 ALTWERASE 标志来改变这种行为。该标志使得前一个标记在遇到第一个非字母数字字符时结束。单词删除字符在处理时被丢弃（即不会传递给进程）。

我们需要为终端设备定义的另一个“字符”是 BREAK 字符。BREAK 实际上不是一个字符，而是异步串行数据传输期间发生的一种条件。BREAK 条件以多种方式通知设备驱动程序，具体取决于串行接口。

> 大多数老式串行终端上都有一个标有 BREAK 的键，用于产生 BREAK 条件，这就是为什么大多数人将 BREAK 视为一个字符的原因。一些较新的终端键盘没有 BREAK 键。在 PC 上，break 键可能被映射用于其他目的。例如，按下 Control-BREAK 可以中断 Windows 命令解释程序。

对于异步串行数据传输，BREAK 是一个持续时长超过发送一个字节所需时间的零值位序列。整个零值位序列被视为一个单独的 BREAK。在第 18.8 节中，我们将看到如何使用 tcsendbreak 函数发送 BREAK。

所有列出的标志都指定了一个或多个我们要开启或清除的位，除非我们将该标志称为掩码。掩码定义了多个组合在一起的位，从中定义一组值。我们为掩码定义一个名称，并为每个值定义一个名称。例如，要设置字符大小，我们首先使用字符大小掩码 CSIZE 将位清零，然后设置 CS5、CS6、CS7 或 CS8 中的一个值。

Linux 和 Solaris 支持的六种延迟值也是掩码：BSDLY、CRDLY、FFDLY、NLDLY、TABDLY 和 VTDLY。有关每个延迟值的长度，请参阅 Solaris 上的 termio(7) 手册页。在所有情况下，延迟掩码为 0 表示没有延迟。如果指定了延迟，OFILL 和 OFDEL 标志决定驱动程序是执行实际延迟，还是发送填充字符。

## 示例

图 18.11 演示了如何使用这些掩码来提取值和设置值。

```
#include "apue.h"
#include <termios.h>
int
main(void)
{
    struct termios term;

    if (tcgetattr(STDIN_FILENO, &term) < 0)
        err_sys("tcgetattr error");

    switch (term.c_cflag & CSIZE) {
    case CS5:
        printf("5 bits/byte\n");
        break;
    case CS6:
        printf("6 bits/byte\n");
        break;
    case CS7:
        printf("7 bits/byte\n");
        break;
    case CS8:
        printf("8 bits/byte\n");
        break;
    default:
        printf("unknown bits/byte\n");
    }
    term.c_cflag &= ~CSIZE;    /* zero out the bits */
    term.c_cflag |= CS8;       /* set 8 bits/byte */
    if (tcsetattr(STDIN_FILENO, TCSANOW, &term) < 0)
        err_sys("tcsetattr error");
    exit(0);
}
```

## CREAD

(c_cflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 如果设置，则接收器被启用，字符可以被接收。

## CRTSCTS

(c_cflag, FreeBSD, Linux, Mac OS X, Solaris) 行为取决于平台。对于 Solaris，如果设置，则启用出站硬件流控制。在其他三个平台上，启用入站和出站硬件流控制（相当于 CCTS_OFLOW | CRTS_IFLOW）。

## CRTS_IFLOW

(c_cflag, FreeBSD, Mac OS X, Solaris) 输入请求发送（RTS）流控制。

## CRTSXOFF

(c_cflag, Solaris) 如果设置，则启用入站硬件流控制。Request-To-Send RS-232 信号的状态控制流控制。

## CSIZE

(c_cflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 该字段是一个掩码，指定发送和接收时每字节的位数。该大小不包括奇偶校验位（如果有）。该掩码定义的字段值分别为 CS5、CS6、CS7 和 CS8，对应每字节 5、6、7 和 8 位。

## CSTOPB

(c_cflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 如果设置，则使用两个停止位；否则，使用一个停止位。

## ECHO

(c_lflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 如果设置，输入字符会被回显到终端设备。输入字符可以在规范模式或非规范模式下回显。

## ECHOCTL

(c_lflag, FreeBSD, Linux, Mac OS X, Solaris) 如果设置且 ECHO 也已设置，则除了 ASCII TAB、ASCII NL 以及 START 和 STOP 字符之外，ASCII 控制字符（范围从 0 到八进制 37（含）的字符）会以 ^X 形式回显，其中 X 是由控制字符加上八进制 100 形成的字符。例如，ASCII Control-A 字符（八进制 1）回显为 ^A，ASCII DELETE 字符（八进制 177）回显为 ^?。如果此标志未设置，则 ASCII 控制字符以其本身形式回显。与 ECHO 标志一样，此标志影响规范模式和非规范模式下控制字符的回显。

请注意，某些系统对 EOF 字符的回显方式不同，因为其典型值是 Control-D。（Control-D 是 ASCII EOT 字符，可能导致某些终端挂断。）请查阅你的手册。

## ECHOE

(c_lflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 如果设置且 ICANON 也已设置，则 ERASE 字符会从显示器上擦除当前行中的最后一个字符。这通常由终端驱动程序写入三字符序列“退格、空格、退格”来完成。

如果支持 WERASE 字符，ECHOE 会使用一个或多个相同的三字符序列来擦除前一个单词。

如果支持 ECHOPRT 标志，则此处描述的 ECHOE 操作假定 ECHOPRT 标志未设置。

## ECHOK

(c_lflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 如果设置且 ICANON 也已设置，则 KILL 字符会从显示器上擦除当前行，或者输出 NL 字符（以强调整行已被擦除）。

如果支持 ECHOKE 标志，此对 ECHOK 的描述假定 ECHOKE 未设置。

## ECHOKE

(c_lflag, FreeBSD, Linux, Mac OS X, Solaris) 如果设置且 ICANON 也已设置，则 KILL 字符会通过擦除行上的每个字符来回显。每个字符的擦除方式由 ECHOE 和 ECHOPRT 标志选择。

## ECHONL

(c_lflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 如果设置且 ICANON 也已设置，则即使 ECHO 未设置，NL 字符也会被回显。

## ECHOPRT

(c_lflag, FreeBSD, Linux, Mac OS X, Solaris) 如果设置且 ICANON 和 ECHO 均已设置，则 ERASE 字符（以及 WERASE 字符，如果支持）会导致所有正在擦除的字符在擦除时被打印出来。这在硬拷贝终端上通常很有用，可以确切地看到正在删除哪些字符。

## EXTPROC

(c_lflag, FreeBSD, Linux, Mac OS X) 如果设置，规范字符处理将在操作系统外部执行。如果串行通信外设卡可以通过执行部分线路规程处理来减轻主机处理器的负担，则可能出现这种情况。使用伪终端时（第 19 章）也可能出现这种情况。

## FFDLY

(c_oflag, XSI, Linux, Solaris) 换页延迟掩码。该掩码的值为 FF0 或 FF1。

## FLUSHO

(c_lflag, FreeBSD, Linux, Mac OS X, Solaris) 如果设置，输出正在被刷新。当我们输入 DISCARD 字符时设置此标志；当我们再次输入 DISCARD 字符时清除此标志。我们也可以通过设置或清除此终端标志来设置或清除此条件。

## HUPCL

(c_cflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 如果设置，当最后一个进程关闭设备时，调制解调器控制线被拉低（即调制解调器连接被断开）。

## ICANON

(c_lflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 如果设置，则规范模式生效（第 18.10 节）。这会启用以下字符：EOF、EOL、EOL2、ERASE、KILL、REPRINT、STATUS 和 WERASE。输入字符被组装成行。

如果未启用规范模式，则读取请求直接从输入队列满足。在收到至少 MIN 个字节或字节间超时值 TIME 到期之前，读取不会返回。更多详细信息请参阅第 18.11 节。
