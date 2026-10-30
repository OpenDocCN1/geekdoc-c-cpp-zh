

```
{ int i; if (client == NULL) client = malloc(NALLOC * sizeof(Client)); else client = realloc(client, (client_size+NALLOC)*sizeof(Client)); if (client == NULL) err_sys("can't alloc for client array"); /* initialize the new entries */ for (i = client_size; i < client_size + NALLOC; i++) client[i].fd = -1; /* fd of -1 means entry available */ client_size += NALLOC; } /* * Called by loop() when connection request from a new client arrives. */ int client_add(int fd, uid_t uid) { int i; if (client == NULL) /* first time we're called */ client_alloc(); again: for (i = 0; i < client_size; i++) { if (client[i].fd == -1) { /* find an available entry */ client[i].fd = fd; client[i].uid = uid; return(i); /* return index in client[] array */ } } /* client array full, time to realloc for more */ client_alloc(); goto again; /* and search again (will work this time) */ } /* * Called by loop() when we're done with a client. */ void client_del(int fd) { int i; for (i = 0; i < client_size; i++) { if (client[i].fd == fd) { client[i].fd = -1;
return;
}
log_quit("can't find client entry for fd %d", fd);
}
```

## Figure 17.27 Functions to manipulate client array

第一次调用 client_add 时，它会调用 client_alloc，后者又调用 malloc 为数组分配十个条目的空间。在这十个条目全部使用后，后续对 client_add 的调用会使 realloc 分配额外的空间。通过这种动态分配空间的方式，我们没有在编译时将客户端数组的大小限制为猜测并写入头文件中的某个值。这些函数在发生错误时会调用 log_ 函数（附录 B），因为我们假设服务器是一个守护进程。

通常服务器将作为守护进程运行，但我们希望提供一个选项，允许它在前台运行，并将诊断信息发送到标准错误。这应该使服务器更容易进行测试和调试，特别是如果我们没有权限读取诊断信息通常写入的日志文件。我们将使用命令行选项来控制服务器是在前台运行还是作为后台守护进程运行。

所有系统上的命令都应遵循相同的约定，因为这使它们更易于使用。如果有人熟悉一个命令的命令行选项形成方式，另一个命令遵循不同约定就会增加出错的机会。

这个问题有时在处理命令行上的空白字符时可见。有些命令要求选项与其参数之间用空白字符分隔，但其他命令要求参数紧跟在选项之后，中间没有任何空格。在没有一致的规则可遵循的情况下，用户要么必须记住所有命令的语法，要么在调用它们时采用试错过程。

单一 UNIX 规范包含一套促进一致命令行语法的约定和指南。它们包括诸如“将每个命令行选项限制为单个字母数字字符”和“所有选项都应以 – 字符开头”之类的建议。

幸运的是，getopt 函数存在，可以帮助命令开发者以一致的方式处理命令行选项。

```
#include <unistd.h>

int getopt(int argc, char * const argv[], const char *options);

extern int optind, opterr, optopt;
extern char *optarg;

Returns: the next option character, or
-1 when all options have been processed
```

argc 和 argv 参数与传递给程序 main 函数的相同。options 参数是一个包含命令支持的选项字符的字符串。如果选项字符后面跟有冒号，则该选项接受参数。否则，选项单独存在。例如，如果命令的用法说明为

```
command [-i] [-u username] [-z] filename
```

我们将把 "iuz:" 作为 options 字符串传递给 getopt。

getopt 函数通常在循环中使用，该循环在 getopt 返回 -1 时终止。在循环的每次迭代中，getopt 会返回处理的下一个选项。应用程序需要自行解决选项冲突；getopt 只是解析选项并强制执行标准格式。

当遇到无效选项时，getopt 会返回问号而不是字符。如果缺少选项的参数，getopt 也会返回问号，但如果 options 字符串的第一个字符是冒号，getopt 会返回冒号而不是。特殊模式 -- 会导致 getopt 停止处理选项并返回 -1。这允许用户提供以减号开头但不是选项的命令参数。例如，如果你有一个名为 -bar 的文件，你不能通过输入

```
rm -bar
```

来删除它，因为 rm 会尝试将 -bar 解释为选项。删除文件的方法是输入

```
rm -- -bar
```

getopt 函数支持四个外部变量。

+   optarg 如果选项接受参数，getopt 在处理选项时会将 optarg 设置为指向选项参数字符串。
+   opterr 如果遇到选项错误，getopt 默认会打印错误消息。要禁用此行为，应用程序可以将 opterr 设置为 0。
+   optind 下一个要处理的字符串在 argv 数组中的索引。它从 1 开始，并在 getopt 处理每个参数时递增。
+   optopt 如果在选项处理期间遇到错误，getopt 会将 optopt 设置为指向导致错误的选项字符串。

open 服务器的 main 函数（图 17.28）定义了全局变量，处理命令行选项，并调用函数 loop。如果我们使用 -d 选项调用服务器，服务器将以交互方式运行而不是作为守护进程。此选项在测试服务器时使用。

```
#include "opend.h"
#include <syslog.h>

int debug, oflag, client_size, log_to_stderr;
char errmsg[MAXLINE];
char *pathname;

Client *client = NULL;
int
main(int argc, char *argv[])
{
    int c;

    log_open("open.serv", LOG_PID, LOG_USER);
   opterr = 0;  /* don't want getopt() writing to stderr */
    while ((c = getopt(argc, argv, "d")) != EOF) {
        switch (c) {
        case 'd':   /* debug */
            debug = log_to_stderr = 1;
            break;

        case '?':
            err_quit("unrecognized option: -%c", optopt);
        }
    }

    if (debug == 0)
        daemonize("opend");
    loop();      /* never returns */
}
```

## Figure 17.28 The server main function, version 2

函数 loop 是服务器的无限循环。我们将展示该函数的两个版本。图 17.29 显示了一个使用 select 的版本；图 17.30 显示了另一个使用 poll 的版本。

```
#include "opend.h"
#include <sys/select.h>

void
loop(void)
{
    int i, n, maxfd, maxi, listenfd, clifd, nread;
    char buf[MAXLINE];
    uid_t uid;
    fd_set rset, allset;

    FD_ZERO(&allset);

    /* obtain fd to listen for client requests on */
    if ((listenfd = serv_listen(CS_OPEN)) < 0)
        log_sys("serv_listen error");
    FD_SET(listenfd, &allset);
    maxfd = listenfd;
    maxi = -1;

for ( ; ; ) {
    rset = allset; /* rset gets modified each time around */
    if ((n = select(maxfd + 1, &rset, NULL, NULL, NULL)) < 0)
        log_sys("select error");

    if (FD_ISSET(listenfd, &rset)) {
        /* accept new client request */
        if ((clifd = serv_accept(listenfd, &uid)) < 0)
            log_sys("serv_accept error: %d", clifd);
        i = client_add(clifd, uid);
        FD_SET(clifd, &allset);
        if (clifd > maxfd)
            maxfd = clifd;  /* max fd for select() */
        if (i > maxi)
            maxi = i;   /* max index in client[] array */
        log_msg("new connection: uid %d, fd %d", uid, clifd);
        continue;
    }

    for (i = 0; i <= maxi; i++) {  /* go through client[] array */
        if ((clifd = client[i].fd) < 0)
            continue;
        if (FD_ISSET(clifd, &rset)) {
            /* read argument buffer from client */
            if ((nread = read(clifd, buf, MAXLINE)) < 0) {
                log_sys("read error on fd %d", clifd);
            } else if (nread == 0) {
                log_msg("closed: uid %d, fd %d",
                    client[i].uid, clifd);
                client_del(clifd);  /* client has closed cxn */
                FD_CLR(clifd, &allset);
                close(clifd);
            } else {
                /* process client's request */
                handle_request(buf, nread, clifd, client[i].uid);
            }
        }
    }
}
```

## Figure 17.29 The loop function using select

此函数调用 serv_listen（图 17.8）为客户端连接创建服务器的端点。函数的其余部分是一个循环，以调用 select 开始。select 返回后可能存在两种情况。

+   1. 描述符 listenfd 可以准备好读取，这意味着新客户端已调用 cli_conn。为处理此情况，我们调用 serv_accept（图 17.9），然后更新客户端数组和新客户端的相关记账信息。（我们跟踪最高描述符号以用于第一个

