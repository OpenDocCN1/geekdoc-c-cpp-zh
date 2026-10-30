

```
81  req.size = htonl(nbytes);
82  if (text)
83      req.flags = htonl(PR_TEXT);
84  else
85      req.flags = 0;
86  if ((len = strlen(fname)) >= JOBNM_MAX) {
87      /*
88       * Truncate the filename (+5 accounts for the leading
89       * four characters and the terminating null).
90       */
91      strcpy(req.jobnm, "... ");
92      strncat(req.jobnm, &fname[len-JOBNM_MAX+5], JOBNM_MAX-5);
93  } else {
94      strcpy(req.jobnm, fname);
95  }
96  /*
97   * Send the header to the server.
98   */
99  nw = writen(sockfd, &req, sizeof(struct printreq));
100 if (nw != sizeof(struct printreq)) {
101     if (nw < 0)
102         err_sys("can't write to print server");
103     else
104         err_quit("short write (%d/%d) to print server",
105                 nw, sizeof(struct printreq));
106 }
```

[81–95] 我们将要打印的文件大小转换为网络字节序后存入头部。如果文件以纯文本形式打印，我们对 `PR_TEXT` 标志做同样的处理。通过将这些整数转换为网络字节序，我们可以在客户端系统上运行打印命令，而打印假脱机守护进程运行在另一台计算机系统上。如果这些系统使用的处理器字节序不同，这些命令仍然可以工作。（我们在 16.3.1 节讨论了字节序。）

我们将作业名称设置为正在打印的文件名。如果名称的长度超过消息中作业名字段所能容纳的长度，我们只复制名称中能容纳的最后部分。这实际上截断了名称的开头部分。在这种情况下，我们会在前面加上省略号，以指示字段中原本有比可容纳的更多的字符。

[96–106] 我们使用 `writen` 向守护进程发送请求头部。（回想一下，我们在图 14.24 中介绍了 `writen` 函数。）`writen` 函数在必要时会多次调用 `write` 来传输指定数量的数据。如果 `writen` 函数返回错误或传输的数据少于我们请求的数量，我们打印错误消息并退出。

```
107  /*
108   * Now send the file.
109   */
110  while ((nr = read(fd, buf, IOBUFSZ)) != 0) {
111      nw = write(sockfd, buf, nr);
112      if (nw != nr) {
113          if (nw < 0)
114              err_sys("can't write to print server");
115          else
116              err_quit("short write (%d/%d) to print server",
117                     nw, nr);
118      }
119  }
120  /*
121   * Read the response.
122   */
123  if ((nr = readn(sockfd, &res, sizeof(struct printresp)) !=
124      sizeof(struct printresp))
125      err_sys("can't read response from server");
126  if (res.retcode != 0) {
127      printf("rejected: %s\n", res.msg);
128      exit(1);
129  } else {
130      printf("job ID %ld\n", (long)ntohl(res.jobid));
131  }
132  }
```

[107–119] 在向守护进程发送头部之后，我们发送要打印的文件。我们每次读取 `IOBUFSZ` 字节的文件数据，并使用 `write` 将这些数据发送给守护进程。与头部一样，如果 `write` 失败或写入的数据少于预期，我们打印错误消息并退出。

[120–132] 一旦我们将要打印的文件发送给打印假脱机守护进程，我们读取守护进程的响应。如果打印请求失败，返回码（`retcode`）将是非零值，因此我们打印响应中包含的文本错误消息。如果请求成功，我们打印作业 ID，以便用户知道将来如何引用该请求。（编写一个取消挂起打印请求的命令留作练习；取消请求中可以使用作业 ID 来标识要从打印队列中移除的作业。参见习题 21.5。）当 `submit_file` 返回到主函数时，我们退出，表示成功。

请注意，守护进程的成功响应并不意味着打印机能够打印该文件；它仅仅意味着守护进程已将打印作业成功添加到队列中。

至此，我们完成了对打印命令的查看。我们要看的最后一个文件是打印假脱机守护进程的 C 源代码文件。

```
1  /*
2   * Print server daemon.
3   */
4  #include "apue.h"
5  #include <fcntl.h>
6  #include <dirent.h>
7  #include <ctype.h>
8  #include <pwd.h>
9  #include <pthread.h>
10 #include <strings.h>
11 #include <sys/select.h>
12 #include <sys/uio.h>
13 
14 #include "print.h"
15 #include "ipp.h"
16 
17 /*
18  * These are for the HTTP response from the printer.
19  */
20 #define HTTP_INFO(x)  ((x) >= 100 && (x) <= 199)
21 #define HTTP_SUCCESS(x) (((x) >= 200 && (x) <= 299))
22 
23 /*
24  * Describes a print job.
25  */
26 struct job {
27  struct job      *next;      /* next in list */
28  struct job      *prev;      /* previous in list */
29  int32_t         jobid;      /* job ID */
30  struct printreq req;        /* copy of print request */
31 };
32 
33 /*
34  * Describes a thread processing a client request.
35  */
36 struct worker_thread {
37  struct worker_thread *next; /* next in list */
38  struct worker_thread *prev; /* previous in list */
39  pthread_t           tid;    /* thread ID */
40  int                 sockfd; /* socket */
41 };
```

[1–19] 打印假脱机守护进程包含了我们之前看到的 IPP 头文件，因为守护进程需要使用该协议与打印机通信。`HTTP_INFO` 和 `HTTP_SUCCESS` 宏定义了 HTTP 请求的状态（回想一下，IPP 构建在 HTTP 之上）。RFC 2616 的第 10 节定义了 HTTP 状态码。

[20–37] `job` 和 `worker_thread` 结构分别用于假脱机守护进程跟踪打印作业和接受打印请求的线程。

```
38  /*
39   * Needed for logging.
40   */
41  int                     log_to_stderr = 0;
42  /*
43   * Printer-related stuff.
44   */
45  struct addrinfo         *printer;
46  char                    *printer_name;
47  pthread_mutex_t         configlock = PTHREAD_MUTEX_INITIALIZER;
48  int                     reread;
49  /*
50   * Thread-related stuff.
51   */
52  struct worker_thread    *workers;
53  pthread_mutex_t         workerlock = PTHREAD_MUTEX_INITIALIZER;
54  sigset_t                mask;
55  /*
56   * Job-related stuff.
57   */
58  struct job              *jobhead, *jobtail;
59  int                     jobfd;
```

[38–41] 我们的日志函数要求我们定义 `log_to_stderr` 变量并将其设置为 0，以强制将日志消息发送到系统日志而不是标准错误。在 `print.c` 中，我们定义了 `log_to_stderr` 并将其设置为 1，尽管我们在用户命令中不使用日志函数。我们可以通过将工具函数拆分为两个独立的文件来避免这种情况：一个用于服务器，一个用于客户端命令。

[42–48] 我们使用全局变量 `printer` 来保存打印机的网络地址。我们将打印机的主机名存储在 `printer_name` 中。`configlock` 互斥锁保护对 `reread` 变量的访问，该变量用于指示守护进程需要重新读取配置文件，这大概是因为管理员更改了打印机或其网络地址。

[49–54] 接下来，我们定义与线程相关的变量。我们使用 `workers` 作为接收客户端文件的线程双向链表的头。该链表由互斥锁 `workerlock` 保护。线程使用的信号掩码保存在变量 `mask` 中。

[55–59] 对于挂起作业的列表，我们定义 `jobhead` 为列表的起始位置，`jobtail` 为列表的尾部。这个列表也是双向链接的，但我们需要将作业添加到列表的末尾，所以我们必须记住一个指向列表尾部的指针。对于工作线程列表，顺序并不重要，所以我们可以将它们添加到列表的头部，不需要记住尾部指针。`jobfd` 是作业文件的文件描述符。

```
60  int32_t                 nextjob;
61  pthread_mutex_t          joblock = PTHREAD_MUTEX_INITIALIZER;
62  pthread_cond_t           jobwait = PTHREAD_COND_INITIALIZER;
63  /*
64   * Function prototypes.
65   */
66  void                     init_request(void);
67  void                     init_printer(void);
68  void                     update_jobno(void);
69  int32_t                  get_newjobno(void);
70  void                     add_job(struct printreq *, int32_t);
71  void                     replace_job(struct job *);
72  void                     remove_job(struct job *);
73  void                     build_gonstart(void);
74  void                     *client_thread(void *);
75  void                     *printer_thread(void *);
76  void                     *signal_thread(void *);
77  ssize_t                  readmore(int, char **, int, int *);
78  int                      printer_status(int, struct job *);
79  void                     add_worker(pthread_t, int);
80  void                     kill_workers(void);
81  void                     client_cleanup(void *);
82  /*
83   * Main print server thread. Accepts connect requests from
84   * clients and spawns additional threads to service requests.
85   *
86   * LOCKING: none.
87   */
88  int
89  main(int argc, char *argv[])
90  {
91      pthread_t               tid;
92      struct addrinfo         *ailist, *aip;
93      int                     sockfd, err, i, n, maxfd;
94      char                    *host;
95      fd_set                  rendezvous, rset;
96      struct sigaction        sa;
97      struct passwd           *pwdp;
```

[60–62] `nextjob` 是下一个要接收的打印作业的 ID。`joblock` 互斥锁保护作业链表以及由 `jobwait` 条件变量表示的条件。

[63–81] 我们声明此文件中其余函数的函数原型。提前这样做使我们可以将这些函数放置在文件中，而不必担心每个函数被调用的顺序。

[82–97] 打印假脱机守护进程的 `main` 函数需要执行两项任务：初始化守护进程，然后处理来自客户端的连接请求。

