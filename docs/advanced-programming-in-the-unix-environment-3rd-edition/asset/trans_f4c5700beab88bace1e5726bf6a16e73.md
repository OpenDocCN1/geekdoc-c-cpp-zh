

## Case C: MIN == 0, TIME > 0

TIME 指定了一个在 read 被调用时启动的读取计时器。 （与 case A 相比，其中非零的 TIME 表示在接收到第一个字节之前不会启动的字节间计时器。）read 在接收到单个字节时返回，或在计时器到期时返回。如果计时器到期，read 返回 0。

## Case D: MIN == 0, TIME == 0

如果有数据可用，read 返回最多请求字节数。如果没有数据可用，read 立即返回 0。

请注意在所有这些情况下，MIN 只是最小值。如果程序请求超过 MIN 字节的数据，则可能接收到多达请求量的数据。这也适用于 MIN 为 0 的 case C 和 D。

Figure 18.19 总结了非规范输入的四种情况。在此图中，nbytes 是 read 的第三个参数（要返回的最大字节数）。

|  | MIN > 0 | MIN == 0 |
|---|---|---|
| TIME > 0 | A: read 在计时器到期前返回 [MIN, nbytes]；如果计时器到期，则返回 [1, MIN)。（TIME = 字节间计时器。调用者可能无限期阻塞。） | C: read 在计时器到期前返回 [1, nbytes]；如果计时器到期，则返回 0。（TIME = 读取计时器。） |
| TIME == 0 | B: read 在数据可用时返回 [MIN, nbytes]。（调用者可能无限期阻塞。） | D: read 立即返回 [0, nbytes]。 |

Figure 18.19 Four cases for noncanonical input

请注意 POSIX.1 允许子脚本 VMIN 和 VTIME 分别具有与 VEOF 和 VEOL 相同的值。事实上，Solaris 为与旧版 System V 保持向后兼容而这样做。这会产生可移植性问题。然而。在从非规范模式切换到规范模式时，我们现在必须恢复 VEOF 和 VEOL 也是。如果 VMIN 等于 VEOF 并且我们不恢复它们的值，当我们将 VMIN 设置为其典型值 1 时，文件结束字符将变为 Control-A。解决此问题的最简单方法是进入非规范模式时保存整个 termios 结构，并在返回规范模式时恢复它。

## Example

Figure 18.20 中的程序定义了 tty_cbreak 和 tty_raw 函数，它们将终端设置为 cbreak 模式和 raw 模式。 （术语 cbreak 和 raw 来自 Version 7 终端驱动程序。）我们可以通过调用 tty_reset 函数将终端重置为其原始状态（这两个函数被调用之前的状态）。

如果我们调用了 tty_cbreak，则在调用 tty_raw 之前需要调用 tty_reset。调用 tty_raw 之后调用 tty_cbreak 也是如此。这提高了在遇到任何错误时终端仍会被留在可用状态的机会。

提供了另外两个函数：tty_atexit 可以被建立为退出处理程序，以确保通过 exit 重置终端模式，并且 tty_termios 返回指向原始规范模式 termios 结构的指针。

```
#include "apue.h"
#include <termios.h>
#include <errno.h>

static struct termios save_termios;
static int          ttysavefd = -1;
static enum { RESET, RAW, CBREAK } ttystate = RESET;

int
tty_cbreak(int fd) /* put terminal into a cbreak mode */
{
    int err;
    struct termios buf;

    if (ttystate != RESET) {
        errno = EINVAL;
        return(-1);
    }
    if (tcgetattr(fd, &buf) < 0)
        return(-1);
    save_termios = buf; /* structure copy */

    /*
     * Echo off, canonical mode off.
     */
    buf.c_lflag &= ~(ECHO | ICANON);

    /*
     * Case B: 1 byte at a time, no timer.
     */
    buf.c_cc[VMIN] = 1;
    buf.c_cc[VTIME] = 0;
    if (tcsetattr(fd, TCSAF LUSH, &buf) < 0)
        return(-1);

    /*
     * Verify that the changes stuck. tcsetattr can return 0 on
     * partial success.
     */
    if (tcgetattr(fd, &buf) < 0) {
        err = errno;
        tcsetattr(fd, TCSAF LUSH, &save_termios);
        errno = err;
        return(-1);
    }
    if ((buf.c_lflag & (ECHO | ICANON)) || buf.c_cc[VMIN] != 1 || buf.c_cc[VTIME] != 0) {

/*
 * Only some of the changes were made. Restore the
 * original settings.
 */
 tcsetattr(fd, TCSAF LUSH, &save_termios);
 errno = EINVAL;
 return(-1);
 }

 ttystate = CBREAK;
 ttysavefd = fd;
 return(0);
 }

 int
 tty_raw(int fd)    /* put terminal into a raw mode */
 {
   int          err;
   struct termios  buf;

   if (ttystate != RESET) {
     errno = EINVAL;
     return(-1);
   }
   if (tcgetattr(fd, &buf) < 0)
     return(-1);
   save_termios = buf; /* structure copy */

   /*
    * Echo off, canonical mode off, extended input
    * processing off, signal chars off.
    */
   buf.c_iflag &= ~(ECHO | ICANON | IEXTEN | ISIG);

   /*
    * No SIGINT on BREAK, CR-to-NL off, input parity
    * check off, don't strip 8th bit on input, output
    * flow control off.
    */
   buf.c_iflag &= ~(BRKINT | ICRNL | INPCK | ISTRIP | IXON);

   /*
    * Clear size bits, parity checking off.
    */
   buf.c_cflag &= ~(CSIZE | PARENB);

   /*
    * Set 8 bits/char.
    */
   buf.c_cflag |= CS8;
   /*
```

```
void
tty_atexit(void)      /* can be set up by atexit(tty_atexit) */
{
    if (ttysavefd >= 0)
        tty_reset(ttysavefd);
}

struct termios *
tty_termios(void)      /* let caller see original tty state */
{
    return(&save_termios);
}
```

Figure 18.20 Set terminal mode to cbreak or raw

我们对 cbreak 模式的定义如下：

- 非规范模式。正如我们在本节开头提到的，该模式关闭了一些输入字符处理。它不会关闭信号处理，因此用户始终可以输入触发终端生成信号的字符之一。请注意，调用者应捕获这些信号；否则，有可能信号会终止程序，并且终端会被留在 cbreak 模式。
- 作为一般规则，每当我们编写更改终端模式的程序时，我们都应捕获大多数信号。这使我们能够在终止之前重置终端模式。

- 回显关闭。

- 一次一个字节的输入。为此，我们将 MIN 设置为 1，TIME 设置为 0。这是 Figure 18.19 中的 case B。read 不会在至少有一个字节可用之前返回。

我们将 raw 模式定义如下：

- 非规范模式。我们还关闭了信号生成字符的处理（ISIG）和扩展输入字符处理（IEXTEN）。此外，我们通过关闭 BRKINT 来禁用 BREAK 字符生成信号。

- 回显关闭。

- 我们在输入上禁用 CR 到 NL 的映射（ICRNL）、输入奇偶校验检测（INPCK）、输入时剥离第八位（ISTRIP）以及输出流控制（IXON）。

- 8 位字符（CS8），并且奇偶校验检查被禁用（PARENB）。

- 所有输出处理都被禁用（OPOST）。

- 一次一个字节的输入（MIN = 1，TIME = 0）。

Figure 18.21 中的程序测试 raw 和 cbreak 模式。

```
#include "apue.h"
static void
sig_catch(int signo)
{
    printf("signal caught\n");
    tty_reset(STDIN_FILENO);
    exit(0);
}
int
main(void)
{
    int     i;
    char    c;
    if (signal(SIGINT, sig_catch) == SIG_ERR)
        err_sys("signal(SIGINT) error");
    if (signal(SIGQUIT, sig_catch) == SIG_ERR)
        err_sys("signal(SIGQUIT) error");
    if (signal(SIGTERM, sig_catch) == SIG_ERR)
        err_sys("signal(SIGTERM) error");
    if (tty_raw(STDIN_FILENO) < 0)
        err_sys("tty_raw error");
    printf("Enter raw mode characters, terminate with DELETE\n");
    while ((i = read(STDIN_FILENO, &c, 1)) == 1) {
        if ((c & 255) == 0177)      /* 0177 = ASCII DELETE */
            break;
        printf("\$0\n", c);
    }
    if (tty_reset(STDIN_FILENO) < 0)
        err_sys("tty_reset error");
    if (i <= 0)
        err_sys("read error");
    if (tty_cbreak(STDIN_FILENO) < 0)
        err_sys("tty_cbreak error");
    printf("\nEnter cbreak mode characters, terminate with SIGINT\n");
    while ((i = read(STDIN_FILENO, &c, 1)) == 1) {
        c &= 255;
        printf("\$0\n", c);
    }
    if (tty_reset(STDIN_FILENO) < 0)
        err_sys("tty_reset error");
    if (i <= 0)
        err_sys("read error");
    exit(0);
}
```

