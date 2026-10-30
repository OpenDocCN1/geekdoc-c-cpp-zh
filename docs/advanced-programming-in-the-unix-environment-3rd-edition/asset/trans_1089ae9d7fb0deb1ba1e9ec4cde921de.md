

# ssize_t **send**(int *sockfd*, const void **buf*, size_t *nbytes*, int *flags*);

<sys/socket.h>

*flags*: MSG_EOR, MSG_OOB, MSG_NOSIGNAL  
　　　 MSG_CONFIRM (Linux 2.3.0),  
　　　 MSG_DONTROUTE (FreeBSD 8.0, Linux 3.2.0,  
　　　　　　　　　　 Mac OS X 10.6.8, Solaris 10),  
　　　 MSG_DONTWAIT (FreeBSD 8.0, Linux 3.2.0,  
　　　　　　　　　　 Mac OS X 10.6.8, Solaris 10),  
　　　 MSG_EOF (FreeBSD 8.0, Mac OS X 10.6.8),  
　　　 MSG_MORE (Linux 3.2.0)

返回：成功时发送的字节数，错误时为 −1

p. 610

# ssize_t **sendmsg**(int *sockfd*, const struct msghdr **msg*, int *flags*);

<sys/socket.h>

*flags*: MSG_EOR, MSG_OOB, MSG_NOSIGNAL  
　　　 MSG_CONFIRM (Linux 2.3.0),  
　　　 MSG_DONTROUTE (FreeBSD 8.0, Linux 3.2.0,  
　　　　　　　　　　 Mac OS X 10.6.8, Solaris 10),  
　　　 MSG_DONTWAIT (FreeBSD 8.0, Linux 3.2.0,  
　　　　　　　　　　 Mac OS X 10.6.8, Solaris 10),  
　　　 MSG_EOF (FreeBSD 8.0, Mac OS X 10.6.8),  
　　　 MSG_MORE (Linux 3.2.0)

返回：成功时发送的字节数，错误时为 −1

p. 611

# ssize_t **sendto**(int *sockfd*, const void **buf*, size_t *nbytes*, int *flags*,
　　　　 const struct sockaddr **destaddr*, socklen_t *destlen*);

<sys/socket.h>

*flags*: MSG_EOR, MSG_OOB, MSG_NOSIGNAL  
　　　 MSG_CONFIRM (Linux 2.3.0),  
　　　 MSG_DONTROUTE (FreeBSD 8.0, Linux 3.2.0,  
　　　　　　　　　　 Mac OS X 10.6.8, Solaris 10),  
　　　 MSG_DONTWAIT (FreeBSD 8.0, Linux 3.2.0,  
　　　　　　　　　　 Mac OS X 10.6.8, Solaris 10),  
　　　 MSG_EOF (FreeBSD 8.0, Mac OS X 10.6.8),  
　　　 MSG_MORE (Linux 3.2.0)

返回：成功时发送的字节数，错误时为 −1

p. 610

# void　　 **setbuf**(FILE *restrict *fp*, char *restrict *buf*);

<stdio.h>

p. 146

# int　　 **setegid**(gid_t *gid*);

<unistd.h>

返回：成功时为 0，错误时为 −1

p. 258

# int　　 **setenv**(const char **name*, const char **value*, int *rewrite*);

<stdlib.h>

返回：成功时为 0，错误时为 −1

p. 212

int        seteuid(uid_t uid);
             <unistd.h>
             返回：成功时为 0，错误时为 −1                                      p. 258

int        setgid(gid_t gid);
             <unistd.h>
             返回：成功时为 0，错误时为 −1                                      p. 256

void       setgrent(void);
             <grp.h>                                                            p. 183

int        setgroups(int ngroups, const gid_t grouplist[]);
             <grp.h>    /* Linux */
             <unistd.h> /* FreeBSD, Mac OS X, and Solaris */
             返回：成功时为 0，错误时为 −1                                      p. 184

void       sethostent(int stayopen);
             <netdb.h>                                                          p. 597

int        setjmp(jmp_buf env);
             <setjmp.h>
             返回：直接调用时为 0，从 longjmp 调用返回时为非零                          p. 215

int        setlogmask(int maskpri);
             <syslog.h>
             返回：之前的日志优先级掩码值                                          p. 470

void       setnetent(int stayopen);
             <netdb.h>                                                          p. 598

int        setpgid(pid_t pid, pid_t pgid);
             <unistd.h>
             返回：成功时为 0，错误时为 −1                                      p. 294

int        setpriority(int which, id_t who, int value);
             <sys/resource.h>                                                   p. 277
             which: PRIO_PROCESS, PRIO_PGRP, PRIO_USER
             返回：成功时为 0，错误时为 −1

void       setprotoent(int stayopen);
             <netdb.h>                                                          p. 598

void       setpwent(void);
             <pwd.h>                                                            p. 180

int setregid(gid_t rgid, gid_t egid);
<unistd.h>
返回：成功时为 0，错误时为 -1
p. 257

int setreuid(uid_t ruid, uid_t euid);
<unistd.h>
返回：成功时为 0，错误时为 -1
p. 257

int setrlimit(int resource, const struct rlimit *rlptr);
<sys/resource.h>
resource: RLIMIT_CORE, RLIMIT_CPU, RLIMIT_DATA, RLIMIT_FSIZE, RLIMIT_NOFILE, RLIMIT_STACK, RLIMIT_AS (FreeBSD 8.0, Linux 3.2.0, Solaris 10), RLIMIT_MEMLOCK (FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8), RLIMIT_MSGQUEUE (Linux 3.2.0), RLIMIT_NICE (Linux 3.2.0), RLIMIT_NPROC (FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8), RLIMIT_NPTS (FreeBSD 8.0), RLIMIT_RSS (FreeBSD 8.0, Linux 3.2.0, Mac OS X 10.6.8), RLIMIT_SBSIZE (FreeBSD 8.0), RLIMIT_SIGPENDING (Linux 3.2.0), RLIMIT_SWAP (FreeBSD 8.0), RLIMIT_VMEM (Solaris 10)
返回：成功时为 0，错误时为 -1
p. 220

void setserver(int stayopen);
<netdb.h>
p. 599

pid_t setsid(void);
<unistd.h>
返回：成功时为进程组 ID，错误时为 -1
p. 295

int setsockopt(int sockfd, int level, int option, const void *val, socklen_t len);
<sys/socket.h>
返回：成功时为 0，错误时为 -1
p. 624

void setspent(void);
<shadow.h>
平台：Linux 3.2.0, Solaris 10
p. 182

int setuid(uid_t uid);
<unistd.h>
返回：成功时为 0，错误时为 -1
p. 256

int setvbuf(FILE *restrict fp, char *restrict buf, int mode, size_t size);
<stdio.h>
mode: _IOFBF, _IOLBF, _IONBF
返回：成功时为 0，错误时为非零
p. 146

void *shmat(int shmid, const void *addr, int flag);
<sys/shm.h>
flag: SHM_RND, SHM_RDONLY
返回：成功时为指向共享内存段的指针，错误时为 -1
p. 574

int shmctl(int shmid, int cmd, struct shmid_ds *buf);
<sys/shm.h>
cmd: IPC_STAT, IPC_SET, IPC_RMID, SHM_LOCK (Linux 3.2.0, Solaris 10), SHM_UNLOCK (Linux 3.2.0, Solaris 10)
返回：成功时为 0，错误时为 -1
p. 573

int shmdt(const void *addr);
<sys/shm.h>
返回：成功时为 0，错误时为 -1
p. 574

int shmget(key_t key, size_t size, int flag);
<sys/shm.h>
flag: IPC_CREAT, IPC_EXCL
返回：成功时为非负共享内存 ID，错误时为 -1
p. 572

int shutdown(int sockfd, int how);
<sys/socket.h>
how: SHUT_RD, SHUT_WR, SHUT_RDWR
返回：成功时为 0，错误时为 -1
p. 592

int sig2str(int signo, char *str);
<signal.h>
返回：成功时为 0，错误时为 -1
平台：Solaris 10
p. 380

int sigaction(int signo, const struct sigaction *restrict act, struct sigaction *restrict oact);
<signal.h>
返回：成功时为 0，错误时为 -1
p. 350

int sigaddset(sigset_t *set, int signo);
<signal.h>
返回：成功时为 0，错误时为 -1
p. 344

int sigdelset(sigset_t *set, int signo);
<signal.h>
返回：成功时为 0，错误时为 -1
p. 344

int sigemptyset(sigset_t *set);
<signal.h>
返回：成功时为 0，错误时为 -1
p. 344

int sigfillset(sigset_t *set);
<signal.h>
返回：成功时为 0，错误时为 -1
p. 344

int sigismember(const sigset_t *set, int signo);
<signal.h>
返回：为真时为 1，为假时为 0，错误时为 -1
p. 344

void siglongjmp(sigjmp_buf env, int val);
<setjmp.h>
此函数永不返回
p. 356

void (*signal(int signo, void (*func)(int)))(int);
<signal.h>
返回：成功时为信号的先前处置，错误时为 SIG_ERR
p. 323

int sigpending(sigset_t *set);
<signal.h>
返回：成功时为 0，错误时为 -1
p. 347

int sigprocmask(int how, const sigset_t *restrict set, sigset_t *restrict oset);
<signal.h>
how: SIG_BLOCK, SIG_UNBLOCK, SIG_SETMASK
返回：成功时为 0，错误时为 -1
p. 346

int sigqueue(pid_t pid, int signo, const union sigval value)
<signal.h>
返回：成功时为 0，错误时为 -1
p. 376

int sigsetjmp(sigjmp_buf env, int savemask);
<setjmp.h>
返回：直接调用时为 0，从 siglongjmp 调用返回时为非零
p. 356

int stat(const char *restrict path, struct stat *restrict buf);
<sys/stat.h>
返回：成功时为 0，错误时为 -1
p. 93

int str2sig(const char *str, int *signo);
<signal.h>
返回：成功时为 0，错误时为 -1
平台：Solaris 10
p. 380

char *strerror(int errnum);
<string.h>
返回：指向消息字符串的指针
p. 15

size_t strftime(char *restrict buf, size_t maxsize, const char *restrict format, const struct tm *restrict tmptr);
<time.h>
返回：若有空间则存储在数组中的字符数，否则为 0
p. 192

size_t strftime_l(char *restrict buf, size_t maxsize, const char *restrict format, const struct tm *restrict tmptr, locale_t locale);
<time.h>
返回：若有空间则存储在数组中的字符数，否则为 0
p. 192

char *strptime(const char *restrict buf, const char *restrict format, struct tm *restrict tmptr);
<time.h>
返回：指向解析的最后一个字符之后的一个字符的指针，否则为 NULL
p. 195

char *strsignal(int signo);
<string.h>
返回：指向描述信号的字符串的指针
p. 380

int symlink(const char *actualpath, const char *sympath);
<unistd.h>
返回：成功时为 0，错误时为 -1
p. 123

int symlinkat(const char *actualpath, int fd, const char *sympath);
<unistd.h>
返回：成功时为 0，错误时为 -1
p. 123

void sync(void);
<unistd.h>
p. 81

