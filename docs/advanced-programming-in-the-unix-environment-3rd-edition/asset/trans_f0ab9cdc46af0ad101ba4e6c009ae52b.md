

ICRNL	(c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 若设置且 IGNCR 未设置，则接收到的 CR 字符会被翻译成 NL 字符。

IEXTEN	(c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 若设置，则会识别并处理扩展的实现定义特殊字符。

IGNBRK	(c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 设置时，输入上的 BREAK 条件会被忽略。参见 BRKINT，了解如何使 BREAK 条件生成 SIGINT 信号或作为数据读取。

IGNCR	(c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 若设置，则接收到的 CR 字符会被忽略。若未设置此标志，则在 ICRNL 标志设置时，可以将接收到的 CR 翻译成 NL 字符。

IGNPAR	(c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 设置时，具有帧错误（除 BREAK 外）的输入字节或具有奇偶校验错误的输入字节会被忽略。

IMAXBEL	(c_iflag, FreeBSD, Linux, Mac OS X, Solaris) 输入队列满时响铃。

INLCR	(c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 若设置，则接收到的 NL 字符会被翻译成 CR 字符。

INPCK	(c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 设置时，启用输入奇偶校验检查。若 INPCK 未设置，则禁用输入奇偶校验检查。

奇偶校验“生成和检测”与“输入奇偶校验检查”是两回事。奇偶校验位的生成和检测由 PARENB 标志控制。设置此标志通常会导致串行接口的设备驱动程序为传出字符生成奇偶校验并验证传入字符的奇偶校验。PARODD 标志决定奇偶校验应为奇数还是偶数。如果输入字符到达时奇偶校验错误，则会检查 INPCK 标志的状态。如果此标志已设置，则会检查 IGNPAR 标志（以查看是否应忽略具有奇偶校验错误的输入字节）；如果不应忽略该字节，则会检查 PARMRK 标志以查看应将哪些字符传递给读取进程。

ISIG	(c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 若设置，则输入字符会与导致生成终端生成信号的特殊字符（INTR、QUIT、SUSP 和 DSUSP）进行比较；若相等，则生成相应的信号。

ISTRIP	(c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 设置时，有效输入字节会被剥离为 7 位。当此标志未设置时，会处理全部 8 位。

IUCLC	(c_iflag, Linux, Solaris) 输入时将大写映射为小写。

IUTF8 (c_iflag, Linux, Mac OS X) 允许字符擦除处理适用于 UTF-8 多字节字符。

IXANY (c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 启用任何字符重新启动输出。

IXOFF (c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 若设置，则启用 start-stop 输入控制。当它注意到输入队列快满时，终端驱动程序会输出 STOP 字符。该字符应被发送数据的设备识别并导致设备停止。稍后，当输入队列中的字符已被处理后，终端驱动程序会输出 START 字符。这应导致设备恢复发送数据。

IXON (c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 若设置，则启用 start-stop 输出控制。当终端驱动程序接收到 STOP 字符时，输出停止。在输出停止期间，下一个 START 字符会恢复输出。若此标志未设置，START 和 STOP 字符会作为普通字符被进程读取。

MDMBUF (c_cflag, FreeBSD, Mac OS X) 根据调制解调器载波标志进行输出流控制。这是 CCAR_OFLOW 标志的旧名称。

NLDLY (c_oflag, XSI, Linux, Solaris) 换行延迟掩码。掩码的值为 NL0 或 NL1。

NOFLSH (c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 默认情况下，当终端驱动程序生成 SIGINT 和 SIGQUIT 信号时，输入和输出队列都会被刷新。此外，当它生成 SIGSUSP 信号时，输入队列会被刷新。若设置 NOFLSH 标志，则在生成这些信号时不会发生这种队列的正常刷新。

NOKERNINFO (c_iflag, FreeBSD, Mac OS X) 设置时，此标志会阻止 STATUS 字符打印前台进程组的信息。然而，无论此标志是否设置，STATUS 字符仍会向前台进程组发送 SIGINFO 信号。

OCRNL (c_oflag, XSI, FreeBSD, Linux, Solaris) 若设置，则在输出时将 CR 映射为 NL。

OFDEL (c_oflag, XSI, Linux, Solaris) 若设置，则输出填充字符为 ASCII DEL；否则为 ASCII NUL。参见 OFILL 标志。

OFILL (c_oflag, XSI, Linux, Solaris) 若设置，则为延迟传输填充字符（ASCII DEL 或 ASCII NUL；参见 OFDEL 标志），而不是使用定时延迟。参见六个延迟掩码：BSDLY、CRDLY、FFDLY、NLDLY、TABDLY 和 VTDLY。

OLCUC (c_oflag, Linux, Solaris) 若设置，则在输出时将小写字符映射为大写字符。

## ONLCR

(c_oflag, XSI, FreeBSD, Linux, Mac OS X, Solaris) 若设置，则在输出时将 NL 映射为 CR-NL。

## ONLRET

(c_oflag, XSI, FreeBSD, Linux, Solaris) 若设置，则在输出时假定 NL 字符执行回车功能。

## ONOCR

(c_oflag, XSI, FreeBSD, Linux, Solaris) 若设置，则在第 0 列不输出 CR。

## ONOEOT

(c_oflag, FreeBSD, Mac OS X) 若设置，则在输出时丢弃 EOT（'D'）字符。这在某些将 Control-D 解释为挂断的终端上可能是必要的。

## OPOST

(c_oflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 若设置，则进行实现定义的输出处理。参见图 18.6，了解 c_oflag 字段的各种实现定义标志。

## OXTABS

(c_oflag, FreeBSD, Mac OS X) 若设置，则在输出时将制表符扩展为空格。这与将水平制表符延迟（TABDLY）设置为 XTABS 或 TAB3 的效果相同。

## PARENB

(c_cflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 若设置，则为传出字符启用奇偶校验生成，并在传入字符上执行奇偶校验检查。奇偶校验为奇数如果 PARODD 已设置；否则为偶数奇偶校验。另请参阅 INPCK、IGNPAR 和 PARMRK 标志的讨论。

## PAREXT

(c_cflag, Solaris) 选择标记或空格奇偶校验。若 PARODD 已设置，则奇偶校验位始终为 1（标记奇偶校验）。否则，奇偶校验位始终为 0（空格奇偶校验）。

## PARMRK

(c_iflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 设置且 IGNPAR 未设置时，具有帧错误（除 BREAK 外）的字节或具有奇偶校验错误的字节会被进程读取为三个字符序列 \377、\0、X，其中 X 为接收到的错误字节。如果 ISTRIP 未设置，则有效的 \377 会作为 \377、\377 传递给进程。如果 IGNPAR 和 PARMRK 都未设置，则具有帧错误（除 BREAK 外）或具有奇偶校验错误的字节会被读取为单个字符 \0。

## TABDLY

(c_oflag, XSI, Linux, Mac OS X, Solaris) 水平制表符延迟掩码。掩码的值为 TAB0、TAB1、TAB2 或 TAB3。

值 XTABS 等于 TAB3。此值会导致系统将制表符扩展为空格。系统假定每八个空格一个制表符停止位，我们无法更改此假设。

## TOSTOP

(c_lflag, POSIX.1, FreeBSD, Linux, Mac OS X, Solaris) 若设置且实现支持作业控制，则当后台进程尝试向其控制终端写入时，会向该进程组发送 SIGTTOU 信号。默认情况下，此信号会停止进程组中的所有进程。如果后台进程正在向控制终端写入并且忽略或阻塞该信号，则终端驱动程序不会生成此信号。

## VTDLY

(c_oflag, XSI, Linux, Solaris) 垂直制表符延迟掩码。掩码的值为 VT0 和 VT1。

## XCASE

(c_lflag, Linux, Solaris) 若设置且 ICANON 也已设置，则终端被假定为仅大写，所有输入都会转换为小写。要输入大写字符，需在其前加上反斜杠。同样，系统通过在其前加上反斜杠来输出大写字符。（此选项标志今天已过时，因为大多数如果不是全部仅大写终端都已消失。）

## 18.6 stty 命令

上一节描述的所有选项都可以通过程序中的 tcgetattr 和 tcsetattr 函数（第 18.4 节）或从命令行（或 shell 脚本）通过 stty() 命令进行检查和更改。此命令只是我们列在图 18.7 中的前六个函数的接口。如果我们使用其 -a 选项执行此命令，它会显示所有终端选项：

```
$ stty -a
speed 9600 baud; 25 rows; 80 columns;
lflags: icanon isig iexten echo echoe -echok echoke -echonl echoctl
        -echoprt -altwerase -noflsh -tostop -flusho pendin -nokerninfo
        -extproc
iflags: -istrip icrnl -inlcr -igncr ixon -ixoff ixany imaxbel -ignbrk
        brkint -inpck -ignpar -parmrk
oflags: opost onlcr -ocrnl -oxtabs -onocr -onlret
cflags: cread cs8 -parenb -parodd hupcl -clocal -cstopb -crtscts
        -dsrflow -dtrflow -mdmbuf
cchars: discard = 'O'; dsusp = 'Y'; eof = 'D'; eol = <undef>;
eol2 = <undef>; erase = 'H'; erase2 = '?'; intr = 'C'; kill = '^U';
line = 'V'; min = 1; quit = ';'; reprint = 'R'; start = '^Q';
status = '^T'; stop = '^S'; susp = '^Z'; time = 0; werase = 'W';
```

